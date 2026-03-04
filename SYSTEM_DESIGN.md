# GEOINT System Design — Deep Dive

## Entity Model (PostgreSQL Schema)

```sql
-- Countries
CREATE TABLE countries (
  iso2        CHAR(2) PRIMARY KEY,
  iso3        CHAR(3),
  name        TEXT,
  region      TEXT,
  subregion   TEXT,
  geojson     JSONB,        -- GeoJSON polygon
  population  BIGINT,
  gdp_usd     BIGINT,
  regime_type TEXT          -- democracy / autocracy / hybrid
);

-- Tension scores (time-series via TimescaleDB)
CREATE TABLE tension_scores (
  time        TIMESTAMPTZ NOT NULL,
  iso2        CHAR(2) REFERENCES countries(iso2),
  score       DECIMAL(5,2),
  component   JSONB,        -- breakdown per sub-score
  level       TEXT          -- critical/high/elevated/moderate
);
SELECT create_hypertable('tension_scores', 'time');

-- Conflict events
CREATE TABLE conflict_events (
  id          UUID PRIMARY KEY,
  event_date  DATE,
  country     CHAR(2),
  event_type  TEXT,         -- battles/explosions/protests/etc
  fatalities  INT,
  lat         DECIMAL,
  lng         DECIMAL,
  source      TEXT,         -- acled/ucdp/gdelt
  raw         JSONB
);

-- Trade flows
CREATE TABLE trade_flows (
  id          SERIAL PRIMARY KEY,
  year        INT,
  reporter    CHAR(2),
  partner     CHAR(2),
  hs_section  TEXT,
  value_usd   BIGINT,
  flow        TEXT          -- export/import
);

-- Energy routes
CREATE TABLE energy_routes (
  id          SERIAL PRIMARY KEY,
  from_iso    CHAR(2),
  to_iso      CHAR(2),
  resource    TEXT,         -- oil/gas/lng/coal/uranium
  volume_mtoe DECIMAL,
  risk_level  TEXT,
  disrupted   BOOLEAN DEFAULT false
);

-- Sanctions
CREATE TABLE sanctions_entities (
  id          UUID PRIMARY KEY,
  list        TEXT,         -- ofac/eu/un/uk
  name        TEXT,
  country     CHAR(2),
  entity_type TEXT,         -- individual/entity/vessel
  programs    TEXT[],
  listed_at   DATE,
  raw         JSONB
);

-- News events
CREATE TABLE news_events (
  id          UUID PRIMARY KEY,
  published   TIMESTAMPTZ,
  title       TEXT,
  summary     TEXT,
  countries   CHAR(2)[],
  sentiment   DECIMAL,      -- -1 to +1
  source      TEXT,
  url         TEXT
);
```

## API Endpoint Design

```
GET  /api/countries              — all countries + current tension score
GET  /api/countries/:iso/score   — tension timeseries (7d/30d/90d)
GET  /api/conflicts              — recent events (bbox filter supported)
GET  /api/trade?reporter=US&partner=CN  — bilateral flows
GET  /api/energy/routes          — all energy corridors + risk
GET  /api/sanctions?country=RU   — sanctions entities by country
GET  /api/news?region=MIDEAST    — filtered news feed
GET  /api/alliances              — graph nodes + edges

WS   /live                       — push: tension updates, breaking news
```

## Caching Strategy (Redis)

```
tension:all          TTL: 300s   — full country tension list
tension:{iso}        TTL: 60s    — individual country score
news:feed            TTL: 30s    — latest 20 news items
trade:corridors      TTL: 3600s  — top trade flows (slow-changing)
energy:routes        TTL: 600s   — energy flow status
sanctions:{country}  TTL: 21600s — sanctions list by country
```

## Scoring Engine (Python)

```python
class TensionScorer:
    WEIGHTS = {
        'conflict_events': 0.30,
        'displacement':    0.15,
        'sanctions':       0.15,
        'incidents':       0.20,
        'news_sentiment':  0.10,
        'arms_transfers':  0.10,
    }

    def score(self, iso2: str, window_days: int = 30) -> float:
        events     = self.acled.get_events(iso2, window_days)
        displaced  = self.unhcr.get_displacement_delta(iso2)
        sanctions  = self.ofac.get_count(iso2)
        incidents  = self.gdelt.get_cameo_events(iso2, ['14','15','19','20'])
        sentiment  = self.gdelt.get_avg_tone(iso2, window_days)
        arms       = self.sipri.get_transfer_index(iso2)

        raw = (
            self.normalize(events)     * self.WEIGHTS['conflict_events'] +
            self.normalize(displaced)  * self.WEIGHTS['displacement'] +
            self.normalize(sanctions)  * self.WEIGHTS['sanctions'] +
            self.normalize(incidents)  * self.WEIGHTS['incidents'] +
            self.normalize(-sentiment) * self.WEIGHTS['news_sentiment'] +
            self.normalize(arms)       * self.WEIGHTS['arms_transfers']
        ) * 100

        regime_mult = 1.15 if self.is_autocracy(iso2) else 1.0
        return min(100, raw * regime_mult)
```

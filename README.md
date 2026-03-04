# 🌐 GEOINT — Global Intelligence Dashboard

> A real-time geopolitical intelligence platform monitoring conflict zones, trade flows, energy dependencies, sanctions regimes, and alliance networks.

**Live prototype:** open `index.html` in any browser — no build step required.

---

## 📁 Repo Structure

```
geoint-dashboard/
├── index.html              # Self-contained prototype (start here)
├── src/
│   ├── components/         # React/Vue UI components (roadmap)
│   ├── data/               # Static seed data & mock fixtures
│   ├── api/                # API client wrappers
│   └── utils/              # Parsers, geo transforms, scoring logic
├── docs/
│   └── SYSTEM_DESIGN.md    # Full architecture doc
└── public/                 # Static assets
```

---

## 🚀 Quickstart

```bash
git clone https://github.com/yourhandle/geoint-dashboard
cd geoint-dashboard
open index.html             # instant — no install needed
```

To run with hot-reload dev server:
```bash
npm install
npm run dev
```

---

## 🗺️ Feature Modules

| Module | Status | Description |
|---|---|---|
| World Map | ✅ MVP | SVG tension zones, hotspots, trade arcs |
| Tension Index | ✅ MVP | 12 conflict zones, scored + ranked |
| Energy Flows | ✅ MVP | 6 resource corridors with risk |
| Intel Feed | ✅ MVP | Rotating news ticker + live feed |
| Trade Corridors | ✅ MVP | Top bilateral flows + status |
| Macro Indicators | ✅ MVP | Global conflict/econ metrics |
| Sanctions Tracker | ✅ MVP | Active regimes by entity count |
| Alliance Network | ✅ MVP | Canvas graph of alliances/rivalries |
| Real API Integration | 🔲 Roadmap | See section below |
| User alerts / watchlist | 🔲 Roadmap | |
| Historical timeline slider | 🔲 Roadmap | |
| AI-generated briefings | 🔲 Roadmap | |

---

## 📡 APIs & Data Sources

### Conflict & Political Risk

| API / Dataset | Provider | Cost | Use |
|---|---|---|---|
| [ACLED API](https://acleddata.com/api/) | ACLED | Free (academic) | Conflict events, fatalities, actor data |
| [GDELT Project](https://www.gdeltproject.org/) | Google/GDELT | Free | Global news events, tone, conflict signals |
| [Uppsala Conflict Data Program](https://ucdp.uu.se/apidocs/) | Uppsala Univ. | Free | Organized violence dataset, battle deaths |
| [Political Terror Scale](https://www.politicalterrorscale.org/) | Academic | Free | Human rights & terror index per country |
| [Fund for Peace FSI](https://fragilestatesindex.org/) | FFP | Free CSV | Fragile states index — 12 indicators |
| [V-Dem Dataset](https://www.v-dem.net/data/) | V-Dem Institute | Free | Democracy, autocratization, elections data |
| [IISS Armed Conflict Survey](https://www.iiss.org/) | IISS | Paid | Professional-grade conflict assessments |

### Trade & Economic

| API / Dataset | Provider | Cost | Use |
|---|---|---|---|
| [UN Comtrade API](https://comtradeapi.un.org/) | UN | Free (100 req/hr) | Bilateral trade flows by HS code |
| [World Bank API](https://datahelpdesk.worldbank.org/knowledgebase/topics/125589) | World Bank | Free | GDP, debt, inflation, FDI by country |
| [IMF Data API](https://datahelp.imf.org/knowledgebase/articles/667681) | IMF | Free | WEO, BOP, financial stability data |
| [WTO Stats API](https://stats.wto.org/) | WTO | Free | Tariff rates, trade agreements, disputes |
| [OECD API](https://data.oecd.org/api/) | OECD | Free | Advanced economy trade & macro |
| [CEPII BACI](http://www.cepii.fr/CEPII/en/bdd_modele/presentation.asp?id=37) | CEPII | Free | Harmonized bilateral trade (annual) |
| [Alpha Vantage](https://www.alphavantage.co/) | Alpha Vantage | Freemium | FX rates, commodity prices, econ indicators |

### Energy & Resources

| API / Dataset | Provider | Cost | Use |
|---|---|---|---|
| [EIA API](https://www.eia.gov/opendata/) | US Gov | Free | Oil, gas, LNG, coal flows and prices |
| [IEA Data](https://www.iea.org/data-and-statistics) | IEA | Free CSV | Global energy supply/demand by source |
| [Kpler API](https://www.kpler.com/) | Kpler | Paid | Real-time tanker & LNG ship tracking |
| [Orbital Insight GO](https://orbitalinsight.com/) | Orbital | Paid | Satellite oil tank fill levels |
| [Ursa Space](https://ursaspace.com/) | Ursa | Paid | SAR satellite supply chain monitoring |
| [USGS Minerals](https://www.usgs.gov/tools/national-minerals-information-center) | US Gov | Free | Critical minerals, rare earths production |
| [FAO FAOSTAT](https://www.fao.org/faostat/en/) | UN FAO | Free | Global food production, exports, prices |

### Sanctions & Legal

| API / Dataset | Provider | Cost | Use |
|---|---|---|---|
| [OFAC SDN List](https://ofac.treasury.gov/specially-designated-nationals-and-blocked-persons-list-sdn-human-readable-lists) | US Treasury | Free | US sanctions entities (XML/CSV) |
| [EU Sanctions List](https://data.europa.eu/data/datasets/consolidated-list-of-persons-groups-and-entities-subject-to-eu-financial-sanctions) | EU | Free | Consolidated EU sanctions XML |
| [UN Security Council Sanctions](https://scsanctions.un.org/search/) | UN | Free | UN-mandated sanctions lists |
| [OpenSanctions](https://www.opensanctions.org/api/) | OpenSanctions | Freemium | Unified global sanctions API |
| [World-Check](https://www.refinitiv.com/en/financial-crime-and-risk-management/know-your-customer/world-check-one) | Refinitiv | Paid | PEP + sanctions commercial API |

### News & Signals

| API / Dataset | Provider | Cost | Use |
|---|---|---|---|
| [NewsAPI](https://newsapi.org/) | NewsAPI | Freemium | Headlines by country/topic |
| [GDELT Events 2.0](https://blog.gdeltproject.org/gdelt-2-0-our-global-world-in-realtime/) | GDELT | Free | Real-time global event stream (BigQuery) |
| [MediaCloud API](https://mediacloud.org/) | Harvard | Free | Media attention & framing by country |
| [Event Registry](https://eventregistry.org/) | Jozef Stefan | Freemium | Structured news events + sentiment |
| [Feedly API](https://developer.feedly.com/) | Feedly | Paid | Curated intelligence source monitoring |
| [Webhose.io](https://webz.io/) | Webz | Paid | Dark web + open web threat signals |

### Geospatial

| API / Dataset | Provider | Cost | Use |
|---|---|---|---|
| [Natural Earth](https://www.naturalearthdata.com/) | Public Domain | Free | Country borders, coastlines (GeoJSON) |
| [MapBox API](https://www.mapbox.com/) | Mapbox | Freemium | Slippy map tiles, geocoding |
| [OpenStreetMap / Overpass](https://overpass-api.de/) | OSM | Free | Infrastructure, ports, pipelines |
| [UNOSAT](https://www.unitar.org/maps/unosat) | UN | Free | Satellite conflict damage assessment |
| [Planet Labs API](https://www.planet.com/explorer/) | Planet | Paid | Daily satellite imagery worldwide |
| [Sentinel Hub](https://www.sentinel-hub.com/) | ESA/Sinergise | Freemium | SAR + optical satellite data |

---

## 🛠️ Tech Stack (Production)

### Frontend

```
Framework:      React 18 + TypeScript
Map:            MapLibre GL JS (open-source Mapbox fork) OR Deck.gl (GPU-accelerated)
Charting:       D3.js (custom) + Recharts (standard charts)
Graph viz:      Sigma.js OR Cytoscape.js (alliance network)
State:          Zustand (global) + React Query (server state + caching)
Styling:        Tailwind CSS + CSS variables
Real-time:      WebSockets via Socket.io client
Build:          Vite
```

### Backend

```
Runtime:        Node.js 20 (primary) + Python 3.12 (data pipeline)
API framework:  FastAPI (Python) for data ingestion
                Express.js (Node) for client-facing REST/WS
Database:       PostgreSQL 16 (structured data + time-series via TimescaleDB)
                Redis 7 (pub/sub, live feed caching, rate-limit tokens)
Search:         Elasticsearch 8 (full-text news search, event indexing)
Queue:          BullMQ (job queues for API polling)
ORM:            Prisma (Node) / SQLAlchemy (Python)
```

### Data Pipeline

```
Ingestion:      Apache Kafka (event streaming from APIs)
Processing:     Apache Spark (batch scoring) OR dbt (SQL transforms)
Orchestration:  Airflow (scheduled pulls) OR Prefect
Storage:        S3 / R2 (raw data lake)
CDN:            Cloudflare (static assets + edge caching)
```

### Infrastructure

```
Cloud:          AWS (primary) — ECS Fargate + RDS + ElastiCache
                OR Fly.io (simpler deployment)
IaC:            Terraform
CI/CD:          GitHub Actions
Monitoring:     Grafana + Prometheus + Sentry
Auth:           Auth0 OR Clerk (JWT-based)
Secrets:        AWS Secrets Manager / Doppler
```

---

## 🏗️ System Design

```
┌─────────────────────────────────────────────────────────────────┐
│                        DATA SOURCES                             │
│  ACLED · GDELT · UN Comtrade · EIA · OFAC · NewsAPI · Kpler    │
└────────────────────────────┬────────────────────────────────────┘
                             │ HTTP pull (cron / webhooks)
                             ▼
┌─────────────────────────────────────────────────────────────────┐
│                     INGESTION LAYER                             │
│         Python workers (FastAPI + BullMQ + Kafka)              │
│   • Rate-limit aware API polling (per-source backoff)          │
│   • Schema normalization → canonical event model               │
│   • Deduplication fingerprinting (content hash)                │
└────────────────────────────┬────────────────────────────────────┘
                             │
                             ▼
┌─────────────────────────────────────────────────────────────────┐
│                      SCORING ENGINE                             │
│          Python (scikit-learn / custom rules)                  │
│   • Tension Score = weighted(conflict events, displacement,    │
│     sanctions, news volume, arms transfers, border incidents)  │
│   • Energy Risk = supply concentration + pipeline dependency   │
│   • Trade Health = tariff exposure + trade balance trend       │
└────────────────────────────┬────────────────────────────────────┘
                             │
              ┌──────────────┴──────────────┐
              ▼                             ▼
┌─────────────────────┐       ┌─────────────────────────┐
│   PostgreSQL +      │       │   Elasticsearch          │
│   TimescaleDB       │       │   (News + Event Search)  │
│   (scores, metrics, │       │                         │
│    time-series)     │       └─────────────────────────┘
└──────────┬──────────┘                    │
           │                               │
           ▼                               ▼
┌─────────────────────────────────────────────────────────────────┐
│                     API GATEWAY (Express)                       │
│   REST:  /api/tension  /api/trade  /api/energy  /api/news      │
│   WS:    ws://live — push updates every 30s                    │
│   Auth:  JWT bearer tokens                                     │
│   Cache: Redis (60s TTL for scores, 10s for live feed)         │
└────────────────────────────┬────────────────────────────────────┘
                             │
                             ▼
┌─────────────────────────────────────────────────────────────────┐
│                    REACT FRONTEND                               │
│   MapLibre GL  ·  D3  ·  Sigma.js  ·  React Query             │
│   • Map renders GeoJSON country features from DB               │
│   • WS listener updates tension colors + news feed in real-time│
│   • React Query polls REST endpoints with stale-while-revalidate│
└─────────────────────────────────────────────────────────────────┘
```

### Tension Scoring Formula

```python
TENSION_SCORE = (
    conflict_events_30d   * 0.30 +   # ACLED/UCDP event count, normalized
    displacement_delta    * 0.15 +   # UNHCR refugee flow change
    sanctions_count       * 0.15 +   # Active OFAC/EU designations
    military_incidents    * 0.20 +   # Border/sea incidents (GDELT CAMEO)
    news_sentiment_neg    * 0.10 +   # GDELT tone score (negative = higher)
    arms_transfers        * 0.10     # SIPRI transfer index
) * regime_multiplier                # Authoritarian states: ×1.15
```

### Data Freshness Targets

| Module | Refresh Rate | Source |
|---|---|---|
| Conflict events | Every 15 min | ACLED realtime |
| News feed | Every 60 sec | NewsAPI + GDELT |
| Trade data | Daily | UN Comtrade |
| Energy prices | Every 5 min | EIA / Alpha Vantage |
| Sanctions | Every 6 hr | OFAC XML diff |
| Tension scores | Every 30 min | Computed from above |
| Satellite imagery | Daily | Planet/Sentinel |

---

## 📦 Phase Roadmap

```
Phase 1 — Static (NOW)
  ✅ HTML prototype with mock data
  ✅ Full UI: map, tension, energy, trade, sanctions, alliances

Phase 2 — Live Data
  □ Connect UN Comtrade + EIA APIs (free tier)
  □ ACLED conflict event ingestion
  □ OFAC/EU sanctions XML parser
  □ GDELT news stream integration
  □ PostgreSQL + Redis backend

Phase 3 — Intelligence Layer
  □ Tension scoring engine (ML-assisted)
  □ Alert system (watchlist + threshold triggers)
  □ Historical timeline slider (30-day playback)
  □ Country comparison mode

Phase 4 — Advanced
  □ AI briefing generator (Claude API — daily country summaries)
  □ Satellite imagery overlays (Planet/Sentinel)
  □ Ship tracking layer (AIS data — Kpler/MarineTraffic)
  □ Dark web signal monitoring
  □ User accounts + saved watchlists
  □ PDF/DOCX export — intelligence brief format
```

---

## 🔑 Environment Variables

```env
# APIs
ACLED_API_KEY=
GDELT_API_KEY=
NEWSAPI_KEY=
EIA_API_KEY=
ALPHA_VANTAGE_KEY=
MAPBOX_TOKEN=
OPENSANCTIONS_KEY=

# Database
DATABASE_URL=postgresql://user:pass@localhost:5432/geoint
REDIS_URL=redis://localhost:6379

# Auth
AUTH0_DOMAIN=
AUTH0_CLIENT_ID=

# Anthropic (AI briefings)
ANTHROPIC_API_KEY=
```

---

## 📄 License

MIT — free to use, fork, and build on.

---

*Built as a geopolitical intelligence prototype. Data shown in the MVP is illustrative. Production deployment requires proper API licensing for commercial use.*

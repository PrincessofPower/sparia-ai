# sparia-ai
Open source, privacy-first platform for monitoring pharmacy access gaps in real time. Built for governments, NGOs, and industry. US, Kenya, and Chile. SDG 3 and SDG 10.
# Sparia AI

**A privacy-first, open source platform for monitoring and closing pharmacy access gaps.**

[![License: Apache 2.0](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![Status: Early Development](https://img.shields.io/badge/Status-Early%20Development-yellow.svg)]()
[![SDG 3](https://img.shields.io/badge/SDG-3%20Good%20Health-green.svg)]()
[![SDG 10](https://img.shields.io/badge/SDG-10%20Reduced%20Inequalities-green.svg)]()

---

## What Sparia AI does

Pharmacies are not secondary healthcare infrastructure. In many countries they are the first and most frequently used point of contact with the healthcare system. When a pharmacy closes, the community that depended on it does not always find out until the door is locked. When access gaps emerge, health systems often detect them through hospitalization data that arrives months too late.

Sparia AI makes pharmacy access gaps visible in real time, tracks whether they are growing or closing, and surfaces early warning signals before communities reach crisis.

It answers three questions:

- **Where** are pharmacy access gaps today?
- **Which communities** are at risk of losing access in the next 90 to 180 days?
- **How does access compare** across countries and populations?

---

## The three gaps Sparia AI closes

| Gap | Problem today | Sparia AI approach |
|-----|--------------|-------------------|
| **Timeliness** | Most monitoring systems update every few years | Continuous scoring updated as new facility data arrives |
| **Foresight** | Tools only map deserts that already exist | Early warning indicators identify at-risk communities before access disappears |
| **Trust** | Data sharing constraints prevent cross-agency collaboration | Federated learning allows joint model improvement without raw data exchange |

---

## Countries

Sparia AI is being developed and validated across three countries with fundamentally different data environments:

**United States** — High-resolution census and facility data. The immediate challenge is rapid chain pharmacy closures concentrated in the lowest-income communities, with existing monitoring systems too slow to track them.

**Kenya** — Approximately 18 percent of Kenya's landmass does not meet WHO criteria for patient access to any health facility. Pharmacies and drug shops are usually the first point of contact for health care services in sub-Saharan Africa. The national facility list does not include registered pharmacies, meaning the true access gap is larger than official data suggests.

**Chile** — Three chain pharmacies control over 90 percent of the market. For patients outside the public system, community pharmacies are the primary pathway to essential medicines. Geographic inequity in access is documented across regions, with rural and isolated areas particularly underserved.

The same core pipeline adapts to all three countries using publicly available, open-licensed data sources.

---

## Architecture

![Sparia AI Architecture](docs/sparia-architecture.svg)

### Layers

**Data Sources**
OpenStreetMap pharmacy data, national health facility registries, census and administrative boundaries, population and socioeconomic indicators.

**Data Pipeline**
Cleaning and standardization, geocoding, country-specific data adapters, missing data handling.

**Geospatial Engine**
Distance and travel-time maps, population coverage metrics, accessibility measures. Powered by NVIDIA RAPIDS cuSpatial for GPU-accelerated spatial analysis.

**Access Gap Scoring**
Threshold-based desert scores, risk categories, equity weighting across demographic groups.

**Early Warning Layer**
Trend modeling, deterioration signals, predictive risk indicators flagging communities 90 to 180 days before crisis.

**Federated Learning Network**
Local model nodes per health agency or country. Shared model weight updates only. No raw data exchange between nodes. Powered by NVIDIA FLARE.

**User Interfaces**
Interactive map dashboard, API endpoints, multilingual natural language agent powered by NVIDIA NeMo (English, Kiswahili, Spanish).

---

## Data sources by country

| Country | Facility data | Population data | Boundaries |
|---------|--------------|-----------------|------------|
| United States | CMS nursing home registry, pharmacy chain public records | US Census Bureau | Census Bureau TIGER |
| Kenya | Ministry of Health 2024 National Facility Census | Kenya National Bureau of Statistics | GADM administrative boundaries |
| Chile | Ministerio de Salud MIDAS pharmacy API | Instituto Nacional de Estadísticas | INE administrative boundaries |

All data sources are publicly available and open-licensed. No individual-level data is collected, stored, or transmitted at any layer.

---

## Technology stack

| Component | Technology | Role |
|-----------|-----------|------|
| Federated learning | NVIDIA FLARE | Cross-border model training without data sharing |
| Spatial analysis | NVIDIA RAPIDS cuSpatial | GPU-accelerated spatial joins and scoring |
| Multilingual agent | NVIDIA NeMo | Natural language policy queries |
| Geospatial processing | GeoPandas, PostGIS | Boundary processing and scoring |
| Pipeline orchestration | Python 3.11, Docker | Local and federated deployment |

---

## Repository structure

```
sparia-ai/
│
├── data/
│   ├── adapters/          # Country-specific data adapters
│   └── samples/           # Sample open datasets for testing
│
├── notebooks/
│   ├── 01_data_pipeline.ipynb
│   ├── 02_geospatial_scoring.ipynb
│   └── 03_flare_simulation.ipynb
│
├── src/
│   ├── ingestion/         # ETL pipelines per country
│   ├── geospatial/        # Spatial analysis and scoring
│   ├── scoring/           # Desert scoring model
│   ├── modeling/          # Early warning and prediction
│   └── api/               # API endpoints and NeMo agent
│
├── docker/
│   ├── flare/             # NVIDIA FLARE simulation setup
│   └── dev/               # Development environment
│
├── docs/
│   ├── sparia-architecture.svg
│   └── data-adapters.md
│
├── LICENSE
├── README.md
└── requirements.txt
```

---

## Roadmap

- [ ] Kenya data pipeline (Ministry of Health 2024 facility census)
- [ ] US data pipeline (CMS nursing home registry + pharmacy records)
- [ ] Chile data pipeline (MIDAS pharmacy API)
- [ ] Geospatial scoring engine (RAPIDS cuSpatial)
- [ ] Access desert scoring model
- [ ] Early warning layer
- [ ] NVIDIA FLARE federated simulation (two virtual nodes)
- [ ] Differential privacy on public-facing outputs
- [ ] NeMo multilingual agent (English, Kiswahili, Spanish)
- [ ] Interactive map dashboard
- [ ] Digital Public Goods Alliance registration
- [ ] National data adapter documentation

---

## Design principles

**Privacy-first.** No individual-level data is collected, stored, or transmitted at any layer of the platform.

**Open and reproducible.** All components are built on open data and open source tools. All code is released under Apache 2.0.

**Globally portable.** The same pipeline works across countries with different data infrastructure. Adding a new country requires writing a data adapter, not rewriting the system.

**Deployable without advanced infrastructure.** Runs locally on a laptop using CPU fallback. No cloud account, no GPU, no proprietary dependencies required.

**Built for decision-makers, not just analysts.** The system is designed for civil servants, public health directors, and NGO program managers who need to act on information, not just receive it.

---

## Evidence base

The pharmacy-as-primary-care claims grounding this project are supported by peer-reviewed literature:

- Njiri et al. Frontiers in Public Health, 2023. PMC10600020. Kenya: pharmacies and drug shops are usually the first point of contact for health care services in sub-Saharan Africa.
- Patients Access to Medicines in Kenya. PMC, 2022. PMC8898182. 18 percent of Kenya's landmass does not meet WHO criteria for patient access. The national facility list does not include registered pharmacies.
- Castillo-Laborde et al. BMC Health Services Research, 2024. PMC11577939. Chile: public sector patients value territorial coverage of primary care; geographic access guarantees access in isolated areas.
- Pharmacypractice.org, 2020. PMC7470236. Chile: three chain pharmacies control over 90 percent of the market. Private patients must purchase medicines from community pharmacies.
- Berenbrok LA et al. Journal of the American Pharmacists Association, 2022. US: millions of Americans live in pharmacy deserts with documented demographic concentration in vulnerable communities.

---

## SDG alignment

- **SDG 3** (Good Health and Well-Being): Monitoring and closing pharmacy access gaps directly supports universal access to essential medicines.
- **SDG 10** (Reduced Inequalities): Equity weighting in the scoring model explicitly surfaces gaps experienced by the most vulnerable populations.
- **SDG 17** (Partnerships for the Goals): Federated learning architecture enables cross-border collaboration between governments, NGOs, and industry without requiring data sharing.

---

## Contributing

Sparia AI is an early-stage open source project and welcomes contributors. Areas where help is most needed:

- Country data adapters (beyond US, Kenya, Chile)
- Geospatial pipeline development
- NVIDIA FLARE simulation configuration
- Dashboard and visualization
- Documentation and translations

Open an issue to start a conversation before submitting a pull request.

---

## About

Sparia AI is built by [Sheera Sabur] and [Fascil Solutions](https://fascilsolutions.com), with Abigail Yohannes, M.S. (NVIDIA-certified data scientist, founder of BASE) serving as technical consultant and data science advisor.

The project is being developed for submission to the Digital Public Goods Alliance and presented at the AI for Good Global Summit 2026 and UN Open Source Week 2026.

---



Apache 2.0. See [LICENSE](LICENSE) for details.

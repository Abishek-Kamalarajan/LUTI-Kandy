# Integrated Land-Use Transport Interaction (LUTI) Model for Sustainable Urban Growth in Kandy

> **Undergraduate Research Project**
> K. Abishek (20GES1432) · Department of Remote Sensing & GIS · Sabaragamuwa University of Sri Lanka
> Supervised by Prof. RMKGSPB Koswatte · April 2026

---

## Overview

This repository contains the full pipeline of a macroscopic LUTI (Land-Use Transport Interaction) model developed for the Kandy district, Sri Lanka (~1,940 km²). The model simulates how four alternative transport policy scenarios shape urban growth, housing affordability, traffic congestion, and transport emissions across a **2026–2046** planning horizon.

The model was built using Python, AequilibraE, and UrbanSim — the same toolchain used in comparable published research (Shen et al. 2020 — Beijing LUTI) — and evaluated against five quantitative indicators using a multi-criteria performance matrix.

---

## Study Area

**Kandy District, Central Province, Sri Lanka**
- Area: ~1,940 km²
- Traffic Analysis Zones (TAZs): 1,202
- Road network: 17,754 links
- Baseline Vehicle Kilometres Travelled (VKT): 20,997,182 veh-km/day
- Baseline trip demand (2026): 949,906 trips/day
- Data sources: Road Development Authority (RDA), National Transport Commission (NTC), Census Department of Sri Lanka (2024)

---

## Scenarios

| Scenario | Description | Key Intervention |
|----------|-------------|-----------------|
| **Baseline** | Do-Nothing — no new transport investment | Reference trajectory |
| **Scenario A** | Kohuwala–Gatambe Highway Bypass | EUR 54.97M road investment |
| **Scenario B** | Bus Rapid Transit (BRT) System | World Bank P172342 — US$75M |
| **Scenario C** | Transit-Oriented Development (TOD) | BRT + upzoning near stations |

---

## Methodology

The model is structured across five phases:

| Phase | Steps | Description |
|-------|-------|-------------|
| Phase 1 | 1–6 | Data acquisition and preprocessing (RDA, NTC, Census) |
| Phase 2 | 7–12 | Transport model setup — OD matrix (gravity model, β=0.11), link assignment, VKT calibration |
| Phase 3 | 13–16 | Historical validation — *deferred (see Limitations)* |
| Phase 4 | 17–21 | Scenario simulation — land-use and transport interaction over 5-year time steps |
| Phase 5 | 22–27 | Output evaluation — sprawl, affordability, congestion, emissions, performance matrix |

### Evaluation Indicators

| Step | Indicator | Method |
|------|-----------|--------|
| 22 | Urban Sprawl | Shannon Entropy Index |
| 23 | Housing Affordability | Housing Affordability Index (HAI = Annual Income / Housing Cost) |
| 24 | Traffic Congestion | Volume-to-Capacity ratio (V/C); Vehicle-Hours of Delay (VHD) |
| 25 | Air Quality & Emissions | COPERT speed-dependent factors — CO₂, NOₓ, PM₂.₅ |
| 26 | Multi-Criteria Comparison | Normalised 0–10 performance matrix |
| 27 | Final Visualisations | Time-series, radar chart, Lorenz curves, spatial maps |

---

## Key Findings

### 1. Urban Sprawl (Shannon Entropy)
All four scenarios exhibit H > 0.97 — reflecting Kandy's inherently dispersed hill-country settlement pattern constrained by valley topography. The inter-scenario entropy spread at 2046 is only 0.001–0.002, meaning transport policy alone cannot significantly reverse sprawl. Strong zoning controls are needed.

### 2. Housing Affordability
HAI values range from 0.33 to 0.37 across all scenarios, classifying Kandy as **Seriously Unaffordable** (PIR ≈ 2.8×) throughout the planning horizon. Scenario C improves affordability through upzoning-driven housing supply increases near BRT stations, but macro-economic factors dominate. Recommendation: Mandatory Affordable Housing Quotas (25% of new units).

### 3. Traffic Congestion
The Highway Bypass (Scenario A) reduces congestion on the bypass corridor but induces demand on feeder roads. BRT-based scenarios (B and C) reduce vehicle kilometres travelled by **12%** through modal shift, delivering measurable V/C improvements network-wide. VHD savings translate to significant economic productivity gains.

### 4. Air Quality & Emissions
BRT scenarios reduce daily CO₂ by approximately **12%** versus baseline through modal shift. The Highway Bypass may worsen emissions through induced demand and higher operating speeds. PM₂.₅ reduction has direct public health co-benefits in Kandy's bowl topography.

### 5. Overall Performance (Composite Score at 2046)

| Scenario | Sprawl | Affordability | Congestion | Emissions | **Composite** |
|----------|--------|---------------|------------|-----------|---------------|
| Baseline (Do-Nothing) | — | — | — | — | lowest |
| Scenario A — Highway Bypass | mid | mid | mid | low | mid |
| Scenario B — BRT System | mid | mid | high | high | high |
| **Scenario C — TOD (BRT + Upzoning)** | **best** | **best** | **best** | **best** | **highest** |

**Scenario C (Transit-Oriented Development) is the recommended policy path.** The World Bank P172342 BRT investment (US$75M) should be coupled with TOD zoning within 800m of BRT stations, affordable housing mandates, and feeder road improvements.

---

### Generated Outputs

| File | Description |
|------|-------------|
| `step22_shannon_entropy.png` | Urban sprawl time series and bar chart |
| `step23_housing_affordability.png` | HAI time series with affordability bands |
| `step24_congestion_metrics.png` | V/C ratio, VHD, and over-capacity links |
| `step25_emissions_timeseries.png` | CO₂, NOₓ, PM₂.₅ time series |
| `step26_performance_matrix.png` | Heatmap and composite score trajectory |
| `step27A_four_panel_dashboard.png` | Full evaluation dashboard |
| `step27B_radar_chart.png` | Multi-criteria radar chart at 2046 |
| `step27C_lorenz_curves.png` | Spatial equity Lorenz curves |
| `step27D_spatial_density_2046.png` | Zone-level population density maps |

---

## Limitations

1. **OD Matrix** — Built using a gravity model (β=0.11, GEH pass rate 87.5%) derived from census trip productions/attractions, not a household travel survey.
2. **Phase 3 deferred** — Historical validation against Landsat land-use imagery (2005–2020) was deferred due to time constraints and unavailability of ground-truth GN-Division survey data. The model is valid as a prospective scenario comparison tool; relative differences between scenarios are internally consistent.
3. **Link capacities** — Network-average estimates (1,800 PCE/hr for arterials). Field measurements on key corridors would improve V/C precision.
4. **HAI proxy** — `land_price` used as a housing cost proxy; residential transaction prices in Kandy City and Peradeniya may be underestimated.
5. **COPERT emission factors** — European-calibrated; may not fully capture Sri Lanka's fleet age profile and road grade effects in hilly terrain.
6. **BRT travel times** — Synthetic values derived from road speeds; actual NTC timetable data was not publicly available.

---

## References

| Study | Relevance |
|-------|-----------|
| Shen et al. (2020) — Beijing LUTI | Direct methodological parallel (AequilibraE + UrbanSim + COPERT) |
| Simmonds (2001) — DELTA LUTI | Conceptual LUTI framework |
| World Bank P172342 (2021) — Kandy BRT | Same study area; confirms BRT impact range |
| Silva & Pinho (2010) | Shannon entropy thresholds for urban sprawl |
| Bertolini et al. (2005) — Node-Place | Theoretical basis for Scenario C (TOD) |

---

## Author

**K. Abishek** (20GES1432)
Department of Remote Sensing & GIS, Faculty of Geomatics
Sabaragamuwa University of Sri Lanka

- LinkedIn: [linkedin.com/in/abishek-kamalarajan](https://www.linkedin.com/in/abishek-kamalarajan/)
- GitHub: [github.com/Abishek-Kamalarajan](https://github.com/Abishek-Kamalarajan)

**Supervisor:** Prof. RMKGSPB Koswatte

---

## License

This project is submitted as part of an undergraduate dissertation at Sabaragamuwa University of Sri Lanka. Please contact the author before reusing any part of this work.

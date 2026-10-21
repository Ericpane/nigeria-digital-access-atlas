# Nigeria Digital Access Atlas

**Mapping Nigeria’s Digital Divide Through Geospatial Data**

[![Live Map](https://img.shields.io/badge/Live%20Map-Vercel-black?style=for-the-badge&logo=vercel)](https://nigeria-digital-access-atlas.vercel.app/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](LICENSE)
[![Colab](https://img.shields.io/badge/Open%20in-Colab-F9AB00?style=for-the-badge&logo=googlecolab)](https://colab.research.google.com/drive/1r7fvj5RhDcEMUoq2am5qP_HK3_Dgtc6Q?usp=sharing)

> **Team Data Knights**  
> Team Lead: Faith Alabetutu · DSN Bootcamp ID: `DSN/Bot/26/0481`  
> DSN AI Bootcamp 2026 · Geospatial Track

---

## Overview

Speed-test data reaches only **~8.2 %** of Nigerians. For the majority of communities, **no measurement exists at all**. The blank spaces are findings themselves.

The **Nigeria Digital Access Atlas** classifies all **774 Local Government Areas (LGAs)** by:

- measured internet speed (Ookla),
- presence of night-time lights (electricity proxy),
- socioeconomic need (Meta Relative Wealth Index).

It then ranks high-priority zones and stress-tests the ranking across **243 combinations** of thresholds. A stable **core of 167 LGAs** (mostly in the north) emerges — home to **41.6 million people**, of whom **39.8 million** live in dark, unmeasured or slow squares. The same core contains **11,824 mapped schools and clinics** in those blind spots.

**Interactive map** → [nigeria-digital-access-atlas.vercel.app](https://nigeria-digital-access-atlas.vercel.app/)

---

## Key Findings

| Insight | Detail |
|---------|--------|
| **Most of Nigeria is invisible to speed tests** | Only ~8 in 100 people live where tests have been recorded. 447 of 774 LGAs (58 %) have none at all. ~150.8 M people (≈70 %) live in areas that are both unmeasured **and** dark on the night-light map. |
| **A northern core stands out** | 167 LGAs remain in the poorest third **and** in a gap group in ≥90 % of 243 threshold combinations. Leading states: Bauchi, Jigawa, Katsina, Zamfara, Sokoto, Kebbi, Yobe, Taraba, Gombe, Benue. |
| **Many schools & clinics sit in the blind spots** | 46,576 of 73,780 mapped facilities (63 %) are in exposed areas; **11,824** of them lie inside the core LGAs. |
| **The “double-deprived” group is fragile** | Only 17 LGAs at base settings; ranges from 2–237 when thresholds change. Prioritise the **stable core**, not a single cut-off. |

### Top 10 Core LGAs by Exposed Population

| Rank | LGA (State)          | Exposed People | Facilities |
|------|----------------------|----------------|------------|
| 1    | Ningi (Bauchi)       | 572 k          | 86         |
| 2    | Toro (Bauchi)        | 508 k          | 211        |
| 3    | Lere (Kaduna)        | 489 k          | 152        |
| 4    | Alkaleri (Bauchi)    | 480 k          | 70         |
| 5    | Fune (Yobe)          | 446 k          | 58         |
| 6    | Maru (Zamfara)       | 445 k          | 110        |
| 7    | Zurmi (Zamfara)      | 428 k          | 98         |
| 8    | Gamjuwa (Bauchi)     | 415 k          | 116        |
| 9    | Danko Wasagu (Kebbi) | 405 k          | 83         |
| 10   | Gamawa (Bauchi)      | 403 k          | 65         |

*(Full top-15 list available on the live map.)*

---

## Methodology (in brief)

1. **Common 1 km grid**  
   Population raster aggregated to ~1 km cells; each cell assigned to one of 774 LGAs by centre-point (matched on unique ID, never name).

2. **Ookla integration**  
   Speed-test tiles (~600 m) matched to grid cells. A cell is “measured” only with ≥3 tests. Speeds are test-weighted medians (resilient to outliers).

3. **Typology**  
   - **Assessable** LGAs (≥3 measured cells): classified by median speed (≥10 Mbps = fast) **and** share of population in lit cells (≥50 % = lit).  
   - Remaining LGAs labelled “Unmeasured, lit” or “Unmeasured, dark” using night lights alone.

4. **Need layer**  
   Meta Relative Wealth Index — poorest third of LGAs flagged as “poor”. Used **only** for prioritisation, never for judging speed or electricity (avoids circularity).

5. **Priority tiers**  
   - **Tier 1** (most urgent): gap in internet **or** electricity **and** among the poorest third.  
   - “Exposed” people / facilities = those in dark cells that are either unmeasured or slow.

6. **Robustness**  
   Full pipeline re-run **243 times** (81 threshold combinations × 3 definitions of “poor”). Core = LGAs that stay in Tier 1 in ≥90 % of runs.

7. **Accuracy safeguards**  
   Distances & areas computed in appropriate projections (EPSG:32632 / Africa Albers). Population totals and three-city overlays verified before any result is trusted.

> **Important principle**  
> Missing data is **not** treated as bad service. Measured poor service is kept separate from places we simply cannot see.

---

## Data Sources

| Dataset | What it adds | Source / Licence |
|---------|--------------|------------------|
| **Speedtest by Ookla** (provided) | Measured mobile speed (backbone layer) | 9,234 tiles · 42,838 tests · CC BY-NC-SA 4.0 |
| **Zenodo OnSSET Nigeria package v1** | Places, people & power layers | DOI [10.5281/zenodo.15265285](https://doi.org/10.5281/zenodo.15265285) · CC BY 4.0 |
| → GADM LGA boundaries | 774 analysis units (Lake Chad removed) | GADM 4.0 |
| → WorldPop population | People per square (216.3 M total) | 2020 estimate |
| → Night-time lights | Electricity-infrastructure proxy | File last modified May 2019 |
| → Health facilities & schools | 73,780 mapped sites (GRID3) | 49,329 health · 24,451 secondary/tertiary schools |
| → HV lines & travel time | Corroboration only (never decides group) | Nigeria SE4ALL portal (Jun 2022) |
| **Meta Relative Wealth Index (Nigeria)** | Socioeconomic need | Meta Data for Good via HDX · ~2021 · CC BY-NC 4.0 · Chi et al. 2022, PNAS |

---

## Repository Contents

```
nigeria-digital-access-atlas/
├── index.html                      # Interactive Leaflet map (deployed on Vercel)
├── Winning_Geospatial_Track.ipynb  # Full analysis notebook
├── LICENSE                         # MIT
└── README.md                       # This file
```

**Colab notebook** (full pipeline + figures):  
https://colab.research.google.com/drive/1r7fvj5RhDcEMUoq2am5qP_HK3_Dgtc6Q?usp=sharing

---

## Interactive Map Features

The live map has three views:

1. **Typology** – six connectivity/electricity classes  
2. **Priority tiers** – Tier-1 core, Tier 1 (non-core), Tier 2, Tier 3  
3. **Data desert** – share of each LGA that remains unmeasured

Hover any LGA for detailed numbers. Side panel lists the top 15 core LGAs plus methods and limitations.

---

## Recommendations

1. **Fund direct field measurements** and request operator coverage data in unmeasured, dark LGAs.
2. **Prioritise the 167 core LGAs** when assessing electricity and internet access together.
3. **Send field teams** to the 11,824 schools and clinics inside the core to verify working electricity and connectivity.
4. **Build priorities from the stable core**, not from any single threshold combination.

---

## Limitations (read carefully)

- Speed tests are **not a census**. A blank cell does **not** mean there is no service.
- Night-time light is a **proxy**, not proof of electricity. 96.9 % of cells read zero light; 89 LGAs (18.9 M people) show none at all. The lights image may pre-date the 2020 population data and appears too dark in parts of the south (e.g. Ebonyi, Cross River) — exposure there is likely overstated.
- LGA-level aggregates can hide large internal variation. An LGA labelled “Connected” only means its *measured* cells are fast.
- We do not know whether any given school or clinic is open or functional. 107,670 primary schools were excluded because they lack coordinates.
- Results show **association**, not causation. All cut-offs (10 Mbps, 50 % lit, radiance 0.33, etc.) are choices — they were stress-tested, not treated as laws of nature.

---

## Reproducibility & Licences

Everything is fully reproducible. The notebook, sources, and licence notes live in this repository. Every number on the map derives from a single results file.

- Map and tables derived from Ookla data retain **Ookla’s CC BY-NC-SA 4.0** terms.
- Other layers follow their respective licences (CC BY 4.0 / CC BY-NC 4.0).
- Code and documentation in this repository are released under the **MIT License**.

---

## Citation

If you use this work, please cite:

```
Team Data Knights (2026). Nigeria Digital Access Atlas: Mapping Nigeria’s Digital Divide Through Geospatial Data.
DSN AI Bootcamp 2026, Geospatial Track. https://github.com/Ericpane/nigeria-digital-access-atlas
```

---

## Team

**Team Data Knights**  
Lead: Faith Alabetutu (`DSN/Bot/26/0481`)

Built during the **DSN AI Bootcamp 2026** Geospatial Hackathon (“Mapping Nigeria’s Digital Divide through Geospatial Data”).

---

## Contact & Links

- 🗺️ Live Atlas → https://nigeria-digital-access-atlas.vercel.app/
- 📓 Colab notebook → https://colab.research.google.com/drive/1r7fvj5RhDcEMUoq2am5qP_HK3_Dgtc6Q?usp=sharing
- 📦 This repository → https://github.com/Ericpane/nigeria-digital-access-atlas

---

*Unmeasured is not unserved. Missing data is a finding.*

# Transport Pathways Versus Dust Sources: A Negative-Control Test of Trajectory-Statistical Attribution in Riyadh, Saudi Arabia

[![Paper Status](https://img.shields.io/badge/Paper-Under%20Review%20(Atmosphere)-orange.svg)]()
[![Code](https://img.shields.io/badge/Code-Available-brightgreen.svg)]()
[![Platform](https://img.shields.io/badge/Runs%20on-Google%20Colab-blue.svg)]()

**Saleh A. Aloraini** and **Abdullah S. Alnasser\***
*Department of Civil Engineering, College of Engineering, Qassim University, Buraydah 51452, Saudi Arabia*
**\*Correspondence:** `as.alnasser@qu.edu.sa`

This repository contains the analysis code for the manuscript above. It is currently under review in *Atmosphere* (MDPI), and this is the revised version.

---

## Overview

Backward-trajectory statistics (PSCF, CWT) are widely used to locate arid-region dust sources. They assume that trajectories separate emission from transport, but that assumption is rarely tested where the local contribution is known. We test it with ten years (2016–2025) of routine METAR observations at Riyadh King Khalid International Airport (OERK). There, present-weather codes separate dust raised at the station (`BLDU`/`BLSA`, "locally raised") from dust in suspension (`DU`/`SA`, “suspension-dominated”).

**Main results**
- **Dust days:** “Suspension-dominated” days outnumbered locally raised days 345 to 179.
- **Indicator model:** ERA5-driven models reproduced the locally raised class better (held-out AUC 0.914 vs 0.765).
- **The 2023–2025 decline:** dust activity fell 85.9% below the 2016–2022 baseline in 2023–2024. A calibrated receptor-side model does not explain the drop: observed dust days were 13–27% of its expectation in every class. Upwind dust availability, transport changes and local surface change remain hypotheses.
- **Negative control:** PSCF and CWT fields were computed from 14,612 HYSPLIT trajectories. The locally raised class serves as an imperfect negative control, because a distant source is not required to explain its dust.
  - In the unmatched and season-matched designs, the control was *more* enriched over the eight a priori candidate regions than the “suspension-dominated” class (p ≤ 0.007).
  - Wind matching removed most regional structure from both classes.
- **Two pitfalls of the conventional workflow:**
  - Endpoint-weighted fields correlate at r ≈ 0.8 even for random class labels.
  - Event-count pooling of wind-matched fields inflates enrichment.

  We therefore use permutation nulls and a stratum-standardized estimator.

---

## Repository contents

| File | Purpose |
|---|---|
| `Riyadh_Dust.ipynb` | One Google Colab notebook that reproduces the paper. It runs from public data to every table and figure, with no stored outputs. |

---

## Data sources (all public)

| Data | Source |
|---|---|
| Hourly METAR, OERK | Iowa Environmental Mesonet, https://mesonet.agron.iastate.edu |
| ERA5 hourly single levels | Copernicus Climate Data Store, https://cds.climate.copernicus.eu |
| HYSPLIT v5.4.2 and GDAS 1° meteorology | NOAA Air Resources Laboratory, https://www.ready.noaa.gov |

The raw data are not redistributed here. The notebook downloads them into the Drive folder described below.

---

## How to run

The notebook uses this Google Drive folder and creates it as it runs:

```
MyDrive/Research/Riyadh_Dust_Source_Attribution/
├── 02_Meteorology/ERA5/        ERA5 downloads and daily receptor series
├── 03_Observations/METAR/      hourly METAR and homogeneity tables
├── 04_Analysis/                CLASS_daily_events.csv (daily class catalogue)
├── 05_HYSPLIT/trajectories/    tdump files (14,612 trajectories)
└── 07_Revision/                tables and figures
```

Run the cells in order. Each step skips work already saved on Drive.

1. **Setup:** mount Drive. If your folder is elsewhere, edit `PROJECT`.
2. **Section 1, Data** (run once; several hours):
   - ERA5 download and daily receptor series
   - METAR download, dust catalogue and homogeneity tests
   - daily dust classes
   - HYSPLIT trajectories
   - indicator models (Table 2)

   HYSPLIT for Linux needs a free NOAA registration. Place the tarball at `05_HYSPLIT/hysplit_linux.tar.gz`.
3. **Section 2, Analysis code:** writes the analysis modules to `/content/rev_pkg`.
4. **Section 3, Results** (a few minutes):
   - Table 1
   - Tables 2–3 (calibrated expectation)
   - Figures 1–6
   - Tables 4, 5 and S1 and Figures 7–8 (trajectory statistics with 1000 permutations)

Outputs go to `07_Revision/outputs/` and `07_Revision/figures/` (PNG, 300 dpi). Random-forest results can differ by about 1% between scikit-learn versions.

**Credentials.** No keys are stored. The ERA5 download asks for your CDS API key at run time.

**Environment.** Standard Colab packages: numpy, pandas, scipy, scikit-learn, statsmodels, matplotlib and xarray. Coastlines (Natural Earth) are downloaded on first use.

---

## Citation

If you use this code, please cite the paper once it is published. The reference will be added here.

## Contact

Abdullah S. Alnasser (`as.alnasser@qu.edu.sa`)

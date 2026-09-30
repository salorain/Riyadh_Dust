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
| `Riyadh_Dust.ipynb` | Main pipeline covering data acquisition, METAR classification, ERA5 processing, the indicator models, HYSPLIT trajectory generation and the original PSCF/CWT analysis. It runs on Google Colab with Google Drive. |
| `Riyadh_Dust_Revision.ipynb` | Revision analyses. It reads files the main pipeline already wrote to Drive, so HYSPLIT is **not** rerun. It covers the class-conditional CWT, mutually exclusive classes, the stratum-standardized estimator, permutation nulls, the calibrated expectation with benchmarks, Tables 1–5 and S1, and Figures 1–8. |

---

## Data sources (all public)

| Data | Source |
|---|---|
| Hourly METAR, OERK | Iowa Environmental Mesonet, https://mesonet.agron.iastate.edu |
| ERA5 hourly single levels | Copernicus Climate Data Store, https://cds.climate.copernicus.eu |
| HYSPLIT v5.4.2 and GDAS 1° meteorology | NOAA Air Resources Laboratory, https://www.ready.noaa.gov |

The raw data are not redistributed here. The notebooks download or read them into the Drive folder described below.

---

## How to run

Both notebooks expect this Google Drive folder, which the main pipeline creates:

```
MyDrive/Research/Riyadh_Dust_Source_Attribution/
├── 02_Meteorology/ERA5/        ERA5 downloads and daily receptor series
├── 03_Observations/METAR/      hourly METAR and homogeneity tables
├── 04_Analysis/                CLASS_daily_events.csv (daily class catalogue)
├── 05_HYSPLIT/trajectories/    tdump files (14,612 trajectories)
├── 06_SourceAttribution/       PSCF/CWT outputs of the main pipeline
└── 07_Revision/                written by Riyadh_Dust_Revision.ipynb
```

If your folder is elsewhere, edit `PROJECT` in cell 1.1 of the revision notebook.

**Revision notebook (minimum run, a few minutes):**
1. Run cell **1.1** to mount Drive, then run every cell of **Section 1**. These only write the analysis modules to `/content/rev_pkg`.
2. Run **2.1** once. It exports per-trajectory endpoint counts from the existing `tdump` files (about 10 min) and skips itself if the export already exists.
3. Run **7.1**, the trajectory re-analysis. It writes Tables 4, 5 and S1 as CSV and Figures 7–8.

These sections are optional:
- 4.1 recreates Table 1.
- 5.1 recreates the calibrated expectation (Tables 2–3).
- 6.1 recreates Figures 1–6.
- 3.1 exports a compact METAR file for an extra CWT intensity.
- 8.x gives a first look at upwind ERA5 fields. It is not used in the paper.

Outputs are written to `07_Revision/outputs/` and `07_Revision/figures/` (PNG, 300 dpi).

**Credentials.** No keys are stored in this repository. ERA5 downloads prompt for your CDS API key at run time. The OpenAQ and NASA Earthdata cells of the main pipeline are exploratory (PM10 and MERRA-2 access tests) and are not needed for the results. To run them, insert your own key where `<YOUR_OPENAQ_API_KEY>` appears, or log in when prompted.

**Environment.** Standard Colab packages: numpy, pandas, scipy, scikit-learn, statsmodels, matplotlib and xarray. Coastlines (Natural Earth) are downloaded on first use.

---

## Citation

If you use this code, please cite the paper once it is published. The reference will be added here.

## Contact

Abdullah S. Alnasser (`as.alnasser@qu.edu.sa`)

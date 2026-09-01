# Transport Pathways Versus Dust Sources: A Null-Control Test of Trajectory-Statistical Attribution in Riyadh, Saudi Arabia

[![Paper Status](https://img.shields.io/badge/Status-Under%20Review-orange.svg)]()
[![Code Status](https://img.shields.io/badge/Code-Pending%20Tentative%20Acceptance-yellow.svg)]()

> **Code Release Notice:** The full codebase—including data preprocessing scripts, HYSPLIT batch trajectory generation, and PSCF/CWT null-control analysis pipelines—will be made publicly available in this repository upon the tentative acceptance of the manuscript.

---

**Saleh A. Aloraini** and **Abdullah S. Alnasser\***  
*Department of Civil Engineering, College of Engineering, Qassim University, Buraydah 51452, Saudi Arabia*  
**\*Correspondence:** `as.alnasser@qu.edu.sa`

---

## **Overview**

Backward-trajectory statistics locate arid-region dust sources on the assumption that trajectories separate emission from transport—an assumption seldom tested where the local contribution is known. This project presents a 10-year (2016–2025) empirical evaluation of trajectory-statistical attribution in Riyadh, Saudi Arabia.

**Key Study Highlights:**
* **Dataset:** 10 years of routine METAR observations at Riyadh distinguishing locally lifted dust (`BLDU`/`BLSA`) from dust in suspension (`DU`/`SA`).
* **Predictive Modeling:** ERA5-driven models reproducing meteorological signatures (held-out AUC 0.914 vs. 0.765).
* **Trajectory Attribution:** Analysis of **14,612 HYSPLIT trajectories** evaluating Potential Source Contribution Function (PSCF) and Concentration-Weighted Trajectory (CWT) fields.
* **Null-Control Framework:** Uses the locally lifted dust class—for which a distant source is not required—as a null control under unmatched, season-matched, and wind-matched backgrounds to evaluate the impact of shared Shamal transport climatology on emitting terrain identification.

---

## **Planned Repository Structure**

Upon public release, this repository will contain:

* `data/` — Processed METAR present-weather classification codes and ERA5 extraction templates.
* `hysplit/` — Automated execution and batch processing scripts for 14,612 backward trajectories.
* `pscf_cwt/` — Code for calculating PSCF and CWT spatial fields across candidate dust source regions.
* `null_control/` — Statistical scripts for running background matching (unmatched, season-matched, wind-matched) and correlation analysis against transport-dominated fields.

---

## **Contact**

For inquiries regarding the manuscript or underlying datasets while the review process is underway, please contact the corresponding author:

**Abdullah S. Alnasser** (`as.alnasser@qu.edu.sa`)

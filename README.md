# Well-Siting-MCDA

**Probabilistic Municipal Well Siting: Spatial Multi-Criteria Decision Analysis (MCDA) and Monte Carlo Uncertainty Quantification**

---

**Authors:** Ehsan Nikfarjam and Mohsen Nikfarjam

*Equal co-authorship. Both authors share intellectual responsibility for the project; lead roles are described under [Attribution](#attribution).*

**Date:** Spring 2025

**Context:** Graduate course project, CIVE 891 Groundwater Geology, University of Nebraska-Lincoln (course instructor: Dr. Erin Haacker). The siting scenario, the client, and the study area are an instructional case, not a real municipal engagement. The prioritization-matrix approach is adapted from Glotfelty (2017); the implementation, scoring code, and uncertainty analysis are the authors' work.

---

## Overview

Local governments face infrastructure siting decisions in which the underlying hydrogeologic and economic data carry real uncertainty. This project builds a reproducible, uncertainty-aware method for that class of decision.

A Python-based Spatial Multi-Criteria Decision Analysis (MCDA) framework weights nine hydrogeologic, logistical, and environmental criteria across 100 candidate well locations on a half-mile grid. Eight locations are screened out by exclusionary "fatal flaw" constraints, and the remaining 92 receive a continuous suitability index ranging from 44.1% to 84.8%. A 250-iteration Monte Carlo simulation then perturbs three uncertain hydrogeologic inputs (hydraulic conductivity, depth to water, and depth to aquifer base) and recomputes the full scoring chain, giving each location a mean and standard deviation of its suitability score, so a decision-maker can see where scores are sensitive to input uncertainty.

The analysis was written up as a course technical report in consulting format, with recommendations for field verification before any siting decision.

---

## Methods

| Component | Detail |
|---|---|
| **Framework** | Weighted Linear Combination (WLC) Spatial MCDA, adapted from Glotfelty (2017) |
| **Criteria** | Nine factors: aquifer transmissivity, well spacing from existing wells, aquifer thickness, land ownership, distance to town, environmental sensitivity, depth to water, depth to aquifer base, soil type |
| **Study area** | 8 km x 8 km, discretized as a 10 x 10 grid at approximately 0.5 mile (800 m) resolution |
| **Locations evaluated** | 100 candidate grid locations; 8 excluded by fatal-flaw screening; 92 scored |
| **Scoring** | Each criterion ranked 1 to 5 and multiplied by an importance weight; total normalized against a maximum possible score of 145 |
| **Suitability index range** | 44.1% to 84.8% across the 92 locations passing fatal-flaw screening |
| **Top-ranked location** | Row 10, Column 10, at 84.8% |
| **Uncertainty analysis** | 250-iteration Monte Carlo simulation (seed 42): normal perturbations of hydraulic conductivity (sd 20%), depth to water (sd 0.5 m), and depth to aquifer base (sd 15%); weights, distances, and fatal flaws held fixed; per-location mean, standard deviation, and coefficient of variation of suitability |
| **Tools** | Python (NumPy, pandas, Matplotlib, Seaborn, cmcrameri, cmocean) |

---

## Scope and Limitations

- **Instructional scenario.** The client, the town, and the stakeholder constraints are a teaching case constructed for CIVE 891. Results are not a siting recommendation for any real municipality.
- **Weights are expert-assigned and fixed.** The importance multipliers encode judgement about relative criterion importance, and the Monte Carlo analysis does not vary them; sensitivity of the ranking to the weights is untested.
- **Fatal-flaw screening is binary.** Eight locations are excluded outright rather than penalized continuously, so the reported index range describes the 92 survivors and not the full grid.
- **Uncertainty is propagated, not estimated from data.** Input uncertainty ranges are assumed and perturbations are independent across cells, so the score distributions express sensitivity to those assumptions rather than measured error. Rank stability (for example, how often each location ranks first) was not computed.
- **No water-quality data.** Salinity and other water-quality risks are outside the analysis and require sampling at any candidate site.

---

## Repository Contents

| File | Description |
|---|---|
| `WellSiting_Analysis_Overview.ipynb` | Documented Jupyter notebook: full MCDA framework, criterion weighting, fatal-flaw screening, suitability scoring, and Monte Carlo uncertainty analysis with visualizations. Figures are embedded and render on GitHub without execution. |

### Viewing the notebook

The notebook renders on GitHub with all 18 figures embedded, so no setup is
needed to read it. Two alternatives, for convenience rather than necessity:

[![nbviewer](https://img.shields.io/badge/render-nbviewer-orange.svg)](https://nbviewer.org/github/Research-Portfolios/Well-Siting-MCDA/blob/main/WellSiting_Analysis_Overview.ipynb)
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Research-Portfolios/Well-Siting-MCDA/blob/main/WellSiting_Analysis_Overview.ipynb)

- **nbviewer** renders it as a clean document with a linkable table of contents: https://nbviewer.org/github/Research-Portfolios/Well-Siting-MCDA/blob/main/WellSiting_Analysis_Overview.ipynb
- **Google Colab** opens a copy in the browser; re-running it requires the course-provided input grids, which are not included in this repository: https://colab.research.google.com/github/Research-Portfolios/Well-Siting-MCDA/blob/main/WellSiting_Analysis_Overview.ipynb

---

## Authors

**Ehsan Nikfarjam**
GitHub: [ehsannikfarjam](https://github.com/ehsannikfarjam)

**Mohsen Nikfarjam**
GitHub: [mohsennikfarjam](https://github.com/mohsennikfarjam)

---

## Attribution

Ehsan Nikfarjam and Mohsen Nikfarjam are equal co-authors. Equal co-authorship reflects shared intellectual responsibility and approval of the work, while the paragraphs below identify the components each led.

**Ehsan Nikfarjam** co-designed the Spatial MCDA framework, led the multi-criteria decision logic and criterion weighting, and led drafting of the co-authored decision-oriented report.

**Mohsen Nikfarjam** co-designed the Spatial MCDA framework, led the hydrogeologic data processing and geospatial quality assurance and quality control that the suitability scoring depends on, and contributed the associated methods and findings to the co-authored report.

The 250-iteration Monte Carlo uncertainty propagation was executed and interpreted jointly. Both authors revised and approved the final report.

---

## Related Outputs

- **Spatiotemporal air pollution exposure and environmental justice analysis:** [github.com/Research-Portfolios/Spatiotemporal-Exposure-Analysis](https://github.com/Research-Portfolios/Spatiotemporal-Exposure-Analysis)

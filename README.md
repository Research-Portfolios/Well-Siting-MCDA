# Well-Siting-MCDA

**Probabilistic Municipal Well Siting: Spatial Multi-Criteria Decision Analysis (MCDA) and Monte Carlo Uncertainty Quantification**

---

**Authors:** Ehsan Nikfarjam and Mohsen Nikfarjam

*Equal co-authorship. Both authors share intellectual responsibility for the project; lead roles are described under [Attribution](#attribution).*

**Date:** Spring 2025

**Context:** Graduate course project, CIVE 891 Groundwater Geology, University of Nebraska-Lincoln (Supervising Instructor: Dr. Erin Haacker). The siting scenario, the client, and the study area are an instructional case, not a real municipal engagement. The framework, the code, and the uncertainty analysis are original work.

---

## Overview

Local governments routinely face infrastructure siting decisions where the underlying hydrogeologic and economic data carry real uncertainty, and where a single misplaced facility can mean years of remediation or project failure. This project builds a reproducible, uncertainty-aware method for that class of decision.

A Python-based Spatial Multi-Criteria Decision Analysis (MCDA) framework weights nine hydrogeologic, logistical, and environmental criteria across 100 candidate well locations on a half-mile grid. Eight locations are screened out by exclusionary "fatal flaw" constraints, and the remaining 92 receive a continuous suitability index ranging from 44.1% to 84.8%. A 250-iteration Monte Carlo simulation then propagates input uncertainty through the MCDA model, replacing point estimates with site-level probability distributions, so a decision-maker can see not just which location ranks highest but how stable that ranking is under uncertainty in the input data.

Findings were translated into a client-ready technical report written for non-technical municipal staff, demonstrating end-to-end science-to-policy translation from geospatial data acquisition through probabilistic siting recommendations.

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
| **Uncertainty analysis** | 250-iteration Monte Carlo simulation (seeded, reproducible) generating site-level probability distributions for probabilistic, risk-informed siting |
| **Tools** | Python (NumPy, Pandas, Matplotlib, Seaborn), ArcGIS Pro |

---

## Scope and Limitations

- **Instructional scenario.** The client, the town, and the stakeholder constraints are a teaching case constructed for CIVE 891. Results are not a siting recommendation for any real municipality.
- **Weights are expert-assigned, not learned.** The importance multipliers encode judgement about relative criterion importance. The Monte Carlo analysis is what tests how sensitive the ranking is to that judgement, and it is the reason the output is a distribution rather than a single answer.
- **Fatal-flaw screening is binary.** Eight locations are excluded outright rather than penalized continuously, so the reported index range describes the 92 survivors and not the full grid.
- **Uncertainty is propagated, not estimated from data.** Input uncertainty ranges are assumed, so the probability distributions express sensitivity to those assumptions rather than measured error.

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
- **Google Colab** opens a runnable copy in the browser, no local install: https://colab.research.google.com/github/Research-Portfolios/Well-Siting-MCDA/blob/main/WellSiting_Analysis_Overview.ipynb

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

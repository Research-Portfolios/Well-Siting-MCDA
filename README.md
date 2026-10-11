# Well-Siting-MCDA

**Municipal Well Siting: Spatial Multi-Criteria Decision Analysis (MCDA) and Monte Carlo Uncertainty Quantification**

---

**Authors:** Ehsan Nikfarjam and Mohsen Nikfarjam

*Equal co-authorship: Ehsan Nikfarjam and Mohsen Nikfarjam contributed equally overall; their roles are listed under [Attribution](#attribution).*

**Date:** Spring 2025

**Context:** Graduate course project, CIVE 891 Groundwater Geology, University of Nebraska-Lincoln (course instructor: Dr. Erin Haacker). The siting scenario, the client, and the study area are an instructional case, not a real municipal engagement. The prioritization-matrix approach is adapted from Glotfelty (2019), as presented in the course's well-siting lesson; the implementation, scoring code, and uncertainty analysis are the authors' work.

---

## Overview

Local governments face infrastructure siting decisions in which the underlying hydrogeologic and economic data carry real uncertainty. This project builds a reproducible, uncertainty-aware method for that class of decision.

A Python-based Spatial Multi-Criteria Decision Analysis (MCDA) framework weights nine hydrogeologic, logistical, and environmental criteria across 100 candidate well locations on a half-mile grid. Eight locations are screened out by exclusionary "fatal flaw" constraints, and the remaining 92 receive a graded suitability index ranging from 44.1% to 84.8%. A 250-iteration Monte Carlo simulation then perturbs three uncertain hydrogeologic inputs (hydraulic conductivity, depth to water, and depth to aquifer base) and recomputes the full scoring chain, giving each location a mean and standard deviation of its suitability score, so a decision-maker can see where scores are sensitive to input uncertainty.

The analysis was written up as a course technical report in consulting format, with recommendations for field verification before any siting decision.

---

## Methods

| Component | Detail |
|---|---|
| **Framework** | Weighted Linear Combination (WLC) Spatial MCDA, adapted from Glotfelty (2019) as presented in the course |
| **Criteria** | Nine factors: aquifer transmissivity, well spacing from existing wells, aquifer thickness, land ownership, distance to town, environmental sensitivity, depth to water, depth to aquifer base, soil type |
| **Study area** | 8 km x 8 km, discretized as a 10 x 10 grid at approximately 0.5 mile (800 m) resolution |
| **Locations evaluated** | 100 candidate grid locations; 8 excluded by fatal-flaw screening; 92 scored |
| **Scoring** | Each criterion ranked 1 to 5 and multiplied by an importance weight; total normalized against a maximum possible score of 145 |
| **Suitability index range** | 44.1% to 84.8% across the 92 locations passing fatal-flaw screening |
| **Top-ranked location** | Row 10, Column 10, at 84.8% |
| **Uncertainty analysis** | 250-iteration Monte Carlo simulation (seed 42): normal perturbations of hydraulic conductivity (sd 20%), depth to water (sd 0.5 m), and depth to aquifer base (sd 15%); weights, distances, and fatal flaws held fixed; per-location mean, standard deviation, and coefficient of variation of suitability |
| **Tools** | Python (NumPy, pandas, Matplotlib, Seaborn) |

---

## Contents

| File | Description |
|---|---|
| `WellSiting_Analysis_Overview.ipynb` | Documented Jupyter notebook: full MCDA framework, criterion weighting, fatal-flaw screening, suitability scoring, and Monte Carlo uncertainty analysis with visualizations. Figures are embedded and render on GitHub without execution. |
| `CONTRIBUTORS.md` | Contributors file: the equal-contribution statement and the authors' shared roles (CRediT), with links to their GitHub profiles. |

---

## Viewing the notebook

The notebook renders on GitHub with all 18 figures embedded, so no setup is
needed to read it. Two alternatives, for convenience rather than necessity:

[![nbviewer](https://img.shields.io/badge/render-nbviewer-orange.svg)](https://nbviewer.org/github/Research-Portfolios/Well-Siting-MCDA/blob/main/WellSiting_Analysis_Overview.ipynb)
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Research-Portfolios/Well-Siting-MCDA/blob/main/WellSiting_Analysis_Overview.ipynb)

- [nbviewer](https://nbviewer.org/github/Research-Portfolios/Well-Siting-MCDA/blob/main/WellSiting_Analysis_Overview.ipynb) renders it as a clean document with a linkable table of contents.
- [Google Colab](https://colab.research.google.com/github/Research-Portfolios/Well-Siting-MCDA/blob/main/WellSiting_Analysis_Overview.ipynb) opens a copy in the browser; re-running it requires the course-provided input grids, which are not included in this repository.

---

## Scope

- **Instructional scenario.** The client, the town, and the stakeholder constraints are a teaching case used in CIVE 891. Results are not a siting recommendation for any real municipality.
- **Weights are set by judgement and fixed.** The importance multipliers encode judgement about relative criterion importance and data certainty, and the Monte Carlo analysis does not vary them; sensitivity of the ranking to the weights is untested.
- **Fatal-flaw screening is binary.** Eight locations are excluded outright rather than penalized continuously, so the reported index range describes the 92 survivors and not the full grid.
- **Uncertainty is propagated, not estimated from data.** Input uncertainty ranges are assumed and perturbations are independent across cells, so the score distributions express sensitivity to those assumptions rather than measured error. Rank stability (for example, how often each location ranks first) was not computed.
- **No water-quality data.** Salinity and other water-quality risks are outside the analysis and require sampling at any candidate site.

---

## Authors

**Ehsan Nikfarjam**
GitHub: [ehsannikfarjam](https://github.com/ehsannikfarjam)

**Mohsen Nikfarjam**
GitHub: [mohsennikfarjam](https://github.com/mohsennikfarjam)

---

## Attribution

Ehsan Nikfarjam and Mohsen Nikfarjam contributed equally overall. Each role below, named as in the Contributor Roles Taxonomy (CRediT), was shared by both authors.

- **Methodology** and **Software:** both authors developed the multi-criteria decision framework in Python.
- **Formal analysis:** both authors implemented the 250-iteration Monte Carlo uncertainty analysis.
- **Visualization:** both authors prepared the notebook and its figures.
- **Writing - original draft:** both authors prepared the course report.

**Credits**

- **Method:** the prioritization-matrix approach is adapted from the method of Glotfelty, M. F. (2019). *The Art of Water Wells: Technical and Economic Considerations for Water Well Siting, Design, and Installation*. NGWA Press (not consulted directly), as presented in the well-siting lesson of the course Groundwater Geology (CIVE 491/891, Spring 2025); the course report cites the method as Glotfelty, M. F. (2017). *The art of water wells*. Marvin Glotfelty Well Seminars. A published review describes the book's first chapter, "Site Selection," as including hydrogeologic and political considerations and an example of a prioritization technique: Haacker, E. (2020). The art of water wells [Review of the book *The art of water wells*, by M. F. Glotfelty]. *Groundwater*, *58*(1), 8. https://doi.org/10.1111/gwat.12954
- **Data:** the seven input grids, the aerial imagery of the study area (USDA Farm Service Agency, August 2008) that gave the reference locations of the town and the existing wells, and the profile logs of wells 'a', 'b', and 'c' were course materials for CIVE 891 and are not included in this repository; as the course report records, hydraulic conductivity was interpolated from a regional USGS report, and elevation was averaged within each grid cell from a USGS National Map digital elevation model.
- **Software:** Python 3.13 (Python Software Foundation License Version 2); NumPy (Harris et al., 2020, doi:10.1038/s41586-020-2649-2; BSD 3-Clause License); pandas (The pandas development team, doi:10.5281/zenodo.3509134; McKinney, 2010, Proceedings of the 9th Python in Science Conference, pp. 56-61, doi:10.25080/Majora-92bf1922-00a; BSD 3-Clause License); Matplotlib (Hunter, 2007, doi:10.1109/MCSE.2007.55; Matplotlib License); Seaborn (Waskom, 2021, doi:10.21105/joss.03021; BSD 3-Clause License); IPython and Jupyter (BSD 3-Clause License).
- **Font:** EB Garamond (SIL Open Font License 1.1), loaded from Google Fonts by the notebook's font-configuration cell.
- **Colours:** colours from ColorBrewer (Cynthia Brewer; Apache-style licence). This product includes color specifications and designs developed by Cynthia Brewer (http://colorbrewer.org/).

---

## Licence

This repository does not yet have a licence; the authors will decide its terms. Until then, GitHub's Terms of Service let others view and fork it on GitHub, and no other reuse is granted.

---

## Related Outputs

- **Spatiotemporal air pollution exposure and environmental justice analysis:** [github.com/Research-Portfolios/Spatiotemporal-Exposure-Analysis](https://github.com/Research-Portfolios/Spatiotemporal-Exposure-Analysis)

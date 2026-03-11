# Spatial Distribution and Molecular Characterization of Lung Cancer in a Northern Israeli Cohort

**A Hospital-Based Epidemiological Study**

Nik Danilov, MD, MPH | School of Public Health, University of Haifa, Israel | 2025

**[View the interactive report](https://DocNikDS.github.io/LUNG_CANCER/Lung_Cancer.html)**

---

## Overview

This repository contains a fully reproducible epidemiological analysis of 94 lung cancer (LC) cases managed at the Lady Davis Carmel Medical Center, Haifa, Israel (2024–2025). The dataset was compiled through systematic review of anonymized electronic medical records extracted from the **Ofek** intra/interhospital medical informatics platform.

The analysis pursues two complementary objectives:

1. To characterize the **spatial distribution** of LC cases across the Haifa District and Northern District of Israel and evaluate whether observed geographic patterns are explained by established confounders — particularly smoking prevalence and population size.

2. To describe the **molecular and histopathological profile** of the cohort and examine how biomarker distributions align with internationally reported data.

The report is authored in **Quarto** and rendered as an **interactive HTML document**, combining spatial epidemiology with clinical-molecular characterization in a single reproducible workflow.

---

## Tech Stack

| Component | Tool |
|---|---|
| Reproducible report | Quarto (.qmd) → HTML |
| Data wrangling | R (`readxl`, `dplyr`) |
| Tables | R (`knitr`, `kableExtra`) |
| Static visualization | R (`ggplot2`, `patchwork`) |
| Interactive maps | R (`leaflet`) |
| Spatial statistics | R (`spdep`) |

---

## Dataset

- **Source:** Anonymized electronic medical records, Lady Davis Carmel Medical Center, Haifa
- **Platform:** Ofek intra/interhospital medical informatics system
- **Sample:** 94 consecutive LC cases, 2024–2025
- **Variables (24):** Demographics (age, sex, ethnic group, locality), smoking status, histopathological diagnosis, immunohistochemistry (PD-L1), next-generation sequencing results (EGFR, KRAS, BRAF, MET, ALK, ROS1, ERBB2, RET, NTRK), mismatch repair status (MSI), tumor mutational burden (TMB)

The full data dictionary is available in the rendered report (Table 1).

---

## Key Findings

### Spatial analysis
- Global Moran's I = −0.008 (permutation p = 0.373) — **no significant spatial autocorrelation**
- LISA identified **three Low–High outliers** (Beitegen, Fassuta, Kiryat Shmona) — no true hotspots
- Stratified Moran's I (smokers only: p = 0.725; non-smokers only: p = 0.626) confirmed **smoking as the primary spatial confounder**
- Population adjustment substantially redistributed apparent risk from large coastal cities to smaller inland localities

### Molecular profiling
- Adenocarcinoma NOS was the dominant subtype (67.0%)
- EGFR, BRAF, and ROS1 alterations occurred exclusively in adenocarcinomas
- Mean TMB ranged from 6.7 mut/Mb (ACA) to 16.1 mut/Mb (NEC)
- Fisher's exact test: no significant difference in smoking prevalence between Jewish and Arab cases (p = 0.815)

---

## Repository Structure

```
LUNG_CANCER/
├── data/
│   └── CarmelMC_LungCancer.xlsx       # Clinical-laboratory dataset (94 cases)
├── EnvEpi_LungCancer_files/           # Quarto HTML supporting files
├── EnvEpi_LungCancer.qmd              # Source document (Quarto/R)
├── EnvEpi_LungCancer.html             # Rendered interactive report
├── EnvEpi_LungCancer.Rproj            # RStudio project file
├── .gitignore
└── README.md
```

---

## Reproducing the Analysis

1. Clone the repository
2. Open `EnvEpi_LungCancer.Rproj` in RStudio
3. Install required R packages:
```r
install.packages(c("readxl", "dplyr", "knitr", "kableExtra",
                   "ggplot2", "patchwork", "tidyr",
                   "leaflet", "spdep"))
```
4. Render the report:
```r
quarto::quarto_render("EnvEpi_LungCancer.qmd")
```

---

## Methodological Note

The analysis demonstrates a key principle of spatial epidemiology: apparent geographic clusters of disease cannot be interpreted at face value. Sequential adjustment for population denominators and behavioral confounders (smoking) overturned an initially significant clustering signal, illustrating how rigorous analysis can prevent misleading conclusions from crude case maps.
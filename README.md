# Device Monitoring, Sample and Element Precision for Analytical Data in handheld pXRF studies - Evaluation in R

## Overview

This repository contains an **R Quarto script** as well as **example data** implementing the workflow described in **Schauer M. Schauer, Chapter 1 - Workflow and Benchmarks for Daily Device Monitoring and Data Precision Assessment in Handheld pXRF Studies. In: Schauer M., Cantin N., and Faucher T., Methodological Innovations in p-XRF studies (Alexandria 2026)**.  

The script was developed by M. Schauer and focuses on:

- identification of reliable elements for quantitative and qualitative interpretation  
- element and sample precision  
- daily device monitoring of handheld pXRF instruments  

The methodology is discussed in more detail in **Schauer 2026**. The script uses example data to demonstrate each calculation step and provides brief explanations of the results for every method applied.


## Citation

If you use this workflow, please cite:

**Schauer, M. (2026), Device Monitoring, Sample and Element Precision for Analytical Data in handheld pXRF studies - Evaluation in R. Supplementary Material to Schauer 2026.**

---

## Motivation

Portable X-ray fluorescence (pXRF) has become a standard tool in archaeological science, yet robust, transparent workflows for precision assessment and routine device monitoring are often lacking.  

This repository provides a reproducible and documented protocol for evaluating pXRF data quality, supporting both methodological transparency and long-term instrument control in archaeological applications.

---

## Workflow Summary

### Precision Assessment

The script evaluates element and sample precision using **LOD, LOQ, and Coefficient of Variation (CV)** metrics (Sections 4 and 5):

- **LOD and LOQ assessment**
  - Monitoring the percentage of `< LOD` values per element.
  - Empirical LOD calculated as `3 × MeanSD`.
  - Empirical LOQ calculated as `3.3 × LOD`.
  - Elements with more than **20 % LOQ violations** are flagged as unreliable for quantitative analysis.
  - Individual and combined monitoring plots are generated.

- **Coefficient of Variation (CV)**
  - CVs are calculated for repeated sample measurements to assess sample precision.
  - A benchmark of **15 % CV** is applied for archaeological pottery, stone, daub, and in-situ soil measurements.
  - For highly homogeneous materials (e.g. obsidian, pressed powders), a **10 % CV** benchmark can be applied.
  - Samples with more than **20 % of reliable elements exceeding the CV benchmark** are flagged.
  - Color-coded spreadsheets and monitoring plots are exported.

> Elements frequently falling below detection or quantification limits may still hold archaeological significance. Such elements should be evaluated carefully and not excluded without considering potential calibration issues or device performance as well as qualitative, interpretative value.

---

### Daily Device Monitoring

To ensure stable and reproducible instrument performance, the script implements:

- **Control Limits**
  - Reference values calculated per mode, matrix, and standard.
  - Upper and lower limits are calcualted.
  - Additional statistics (CV, SEM, median) are provided.
  - Optional inclusion of empirical LOD and LOQ.

- **Shewhart Control Charts**
  - Used to monitor short-term (`s-drift`) and long-term (`l-drift`) instrument drift.

- **Relative Percentage Difference (%RD)**
  - Evaluates analytical accuracy.
  - Acceptable range defined as **−10 % to +10 %**.
  - Results exported as spreadsheets and visualised with plots.

---

## Usage

### Running the Script

1. Open the project in RStudio.

2. Source the Quarto (`.qmd`) file.

3. Set the working directory as indicated in the script (Section 3).

4. Install and load all required packages (Section 2).

The script runs without errors as long as the predefined data structure is maintained.

---

## Output

The workflow generates:

- LOD, LOQ, and CV monitoring plots  
- Summary tables of element and sample precision
- Spreadsheets for precision diagnostics  
- Control limit reference tables  
- Shewhart Control Charts  
- Relative Percentage Difference (%RD) plots and exports  

All outputs are suitable for precision documentation, reporting, and routine instrument monitoring.

---

## Data and Standards

The example dataset includes:

- Experimental pottery samples produced within the scope of ESP 476  
- Reference standards supplied by the manufacturer:
  - SiO₂  
  - Mudrock Standard  
  - SdAR-M2 (International Association of Geoanalysts, 2017)  

Values reported by the device as `< LOD` are replaced with a placeholder value of `0.0000001` to preserve data structure and allow downstream calculations.

---

## Device and Measurement Parameters

Measurements were conducted using a **Bruker Tracer 5g** handheld pXRF (serial no. 900G6390) of the Vienna Institute for Archaeological Science (VIAS) in *MudrockDual* mode:

- Major: 15 kV / 27.9 μA, no filter, 60 s  
- Trace: 40 kV / 38.85 μA, Ti 25 μm / Al 300 μm, 60 s  

The device is equipped with a 20 mm² silicon drift detector (SDD) with a graphene window.

Measurements were carried out between February and May 2025 under controlled environmental conditions.

---

## Packages

This script uses the following R packages:

- basictabler  
- dplyr  
- ggpubr  
- ggplot2  
- openxlsx  
- purrr  
- qcc  
- readr  
- tidyr  
- stringr  

All packages must be installed prior to execution.

---

## License

GPL-3.0

---

## Funding

This research was funded by the **Austrian Science Fund (FWF) ESPRIT Projekt 476 *Standardising Portable X-ray Fluorescence for Archaeometry* ([Schauer 2023](https://www.fwf.ac.at/forschungsradar/10.55776/ESP476))**.

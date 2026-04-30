# Convective Cooling Study – Data Processing & Analysis

## Overview

This repository contains the data processing and analysis pipeline for a study investigating the effect of **local dorsal convective cooling** on:

- Skin temperature
- Microclimate temperature and humidity
- Thermophysiological responses

The workflow is structured to transform raw sensor data into:
- Clean time series
- Phase-based features
- Descriptive statistics
- Mechanistic visualizations

---

## Experimental Design

Each subject performs multiple protocols under different conditions:

- `no_wind`
- `wind_low`
- `wind_high`

Each protocol includes sequential phases:

1. standing_1  
2. walk_low_1  
3. walk_mod_1  
4. walk_low_2  
5. walk_mod_2  
6. standing_2  

---

##  Repository Structure

```text
data/
├── raw/                          # Raw sensor data
├── processed/
│   ├── aggregated_by_signal/    # Per-signal datasets
│   ├── analysis/                # Merged datasets (long & wide)
│   └── features/                # Phase features & baseline

reports/
├── descriptives/                # Tables
├── figures/                     # Time series plots
└── mechanistic_plots/           # Scatter & relationships

scripts/
├── make_dataset.py
├── prepare_analysis_dataset.py
├── run_descriptive_analysis.py
├── extract_phase_features.py
├── plot_phase.py
├── statistic.py
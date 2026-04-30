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


---

## Workflow

### 1. Raw Data Processing

Run:
```bash
scripts/make_dataset.py
```

This script:
- Reads raw CSV files
- Extracts a 70-minute window per test
- Outputs one dataset per signal

Output:
```data/processed/aggregated_by_signal/
```

---

### 2. Dataset Construction

Run:
```bash
scripts/prepare_analysis_dataset.py
```

This script:
- Merges signals into unified datasets
- Aligns time series
- Adds elapsed time and phase labels

Output:
```data/processed/analysis/
- all_signals_long.csv
- analysis_dataset_wide.csv
```

---

### 3. Descriptive Analysis

Run:
```bash
scripts/run_descriptive_analysis.py
```

This script:
- Computes descriptive statistics
- Generates time series plots
- Generates individual subject plots

Output:
```reports/descriptives/
reports/figures/
``` 

---

### 4. Phase-Based Feature Extraction

Run:
```bash
scripts/extract_phase_features.py
```

This script:

**Mean skin temperature**
- Computed as average of:
  - t_neck
  - t_dorsal
  - t_hand
  - t_shin

**Baseline**
- Defined as mean of the last 2 minutes of standing_1

**Phase features**
For each subject, condition, phase and signal:
- mean
- standard deviation
- median
- min / max
- slope
- delta (start to end)
- delta vs baseline

Output:
```data/processed/features/
- analysis_dataset_with_tsk.csv
- baseline_values.csv
- phase_features_long.csv
```

Additionally, this script:
- Aligns signals directly from raw aggregated data
- Avoids wide dataset misalignment issues
- Generates scatter plots for:

Temperature:
- t_microclimateback vs t_dorsal

Humidity:
- rh_microclimateback vs rh_dorsal

Output:
```reports/mechanistic_plots/
- t_microclimateback_vs_t_dorsal.png
- rh_microclimateback_vs_rh_dorsal.png
```

---

### 5. Mechanistic Analysis

Run:
```bash
scripts/statistic.py
``` 
Still in development, this script will perform:
- Statistical tests on phase features
- Correlation analyses between microclimate and skin responses
- Generate mechanistic visualizations


---

## Current Outputs

- Time series (mean and individual)
- Phase-based statistical features
- Baseline-normalized values
- Mechanistic scatter plots

---

## Known Limitations

- Small sample size (statistical models not stable yet)
- Sensor signals may not be perfectly synchronized
- Temperature shows complex, non-linear behavior
- Humidity shows stronger linear coupling

---

## Next Steps

Planned analyses:

- Linear Mixed Models (LMM)
- Repeated measures ANOVA
- Phase-dependent effects
- Dose-response analysis

Future integrations:

- Subjective thermal perception
- Back thermography
- Synthetic indices:
  - Cooling Benefit Index (CBI)
  - Recovery Efficiency (RE)
  - Microclimate Relief Index

---

## Key Research Questions

- Does convective cooling improve comfort before global temperature changes?
- Does microclimate change precede skin response?
- Is the cooling effect phase-dependent?
- Is there a dose-response with fan intensity?

---

## Notes

- Mechanistic plots must be built from aligned signals
- Baseline normalization is critical for comparisons
- Individual plots are essential for data validation

---



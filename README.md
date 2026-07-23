# DataFest 2025 — Commercial Leasing & Market Dynamics (ASU Hackathon)
 
**Project:** exploratory analysis, geospatial visualization, clustering, and baseline predictive modeling of commercial leasing across major U.S. markets (Manhattan focus).

---

## Quick summary
We analyze commercial leasing, price/availability, and unemployment data to:
- Visualize spatial leasing patterns (interactive folium maps; Manhattan primary demo).
- Trace time‑series dynamics of leasing, occupancy, rent, and availability (pre/during/post COVID).
- Identify geographic clusters of leasing activity and per‑industry clusters.
- Provide a baseline KNN classifier predicting industry from geolocation (latitude/longitude).

This repository contains cleaned, non‑proprietary derivatives and scripts to reproduce analyses on the supplied example data. Do not commit API keys or proprietary/PII data.

---

## Table of contents
- [Data](#data)
- [Project structure](#project-structure)
- [Methods (short)](#methods-short)
- [Key outputs](#key-outputs)
- [Reproducibility artifacts](#reproducibility-artifacts)
- [Files included](#files-included)
- [License & contact](#license--contact)

---

## Data
Place input files under `data/`. Expected CSVs (examples included where permitted):
- `data/Leases.csv` — lease-level records (leasedSF, address, city, state, market, year, quarter, internal_industry, internal_class, RBA, leasing, available_space, rent).
- `data/Price and Availability Data.csv` — market/year/class price & availability.
- `data/Major Market Occupancy Data-revised.csv` — quarterly occupancy proportions.
- `data/Unemployment.csv` — monthly unemployment by state.

See `data/README.md` for provenance, licensing notes, and guidance on using restricted/proprietary inputs.

---

## Project structure
- `README.md` — this file.
- `Thesis_description.md` — extended project description (detailed).
- `requirements.txt` — Python dependencies.
- `run_summary.json` — run metadata template and canonical run output.
- `src/` — scripts:
  - `run_pipeline.py` — orchestrates the pipeline.
  - `geocode.py` — safe, caching geocoder (uses environment variable for API key).
  - `preprocess.py`, `visualize.py`, `cluster.py`, `model.py` — modular steps.
- `notebooks/` — reproducible notebooks (e.g., `reproduce_example.ipynb`).
- `data/` — input CSVs and `data/geocode_cache.csv`.
- `maps/` — saved folium HTML maps.
- `figures/` — saved PNG figures.
- `outputs/` — model outputs, CSVs, and exported results.
- `.env.example`, `.gitignore`, `LICENSE`.

---

## Methods (short)
- Data cleaning and QC; date construction for monthly and quarterly series.
- Geocoding via LocationIQ with caching, retries/backoff, and session reuse.
- Visualizations: folium for maps; matplotlib/seaborn for time series and heatmaps.
- Clustering: KMeans on standardized coordinates; elbow and silhouette checks; per‑industry clustering.
- Predictive baseline: KNN classifier on scaled lat/lon (train/test, cross‑validation, confusion matrix).

---

## Key outputs
- `maps/manhattan_industry_map.html` — interactive Manhattan map colored by industry.
- `maps/industry_maps/*.html` — per‑industry cluster maps.
- `figures/` — saved PNGs (correlation heatmap, time series, cluster visualizations).
- `outputs/metrics.csv` — model metrics and CV results.
- `run_summary.json` — run metadata (commit SHA, date, environment, seed, inputs/outputs).

---

## Reproducibility artifacts
- `requirements.txt` — package list for quick setup (pin versions for strict reproducibility).
- `run_summary.json` — automated record of the canonical run (git commit, date, seed, file checksums).
- `data/geocode_cache.csv` — cached lat/lon for addresses to avoid re‑querying the geocode API.

---

## Files included
See repository structure. Do not commit API keys or sensitive data. `data/example/` contains a small synthetic sample allowing quick reproduction without external APIs.

---

## License & contact
License: MIT (see LICENSE).  
Contact: Vanya Murzin — evawnmurzin@gmail.com

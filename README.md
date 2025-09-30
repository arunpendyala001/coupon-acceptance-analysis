# coupon-acceptance-analysis

Analysis of customer coupon acceptance behavior using Python, pandas, and data visualization.

## Overview

This repository explores factors influencing whether drivers accept location-based coupons, using the UCI ML dataset collected via Mechanical Turk. The analysis lives in `prompt.ipynb`, where we inspect distributions, address missing values, and visualize patterns across user, contextual, and coupon features.

## Repository Structure

- `data/coupons.csv` — Source dataset (~12.6k rows, 26 columns).
- `prompt.ipynb` — Main Jupyter notebook with the analysis workflow and prompts.
- `images/` — Supporting images/assets (e.g., screenshots used in documentation).
- `LICENSE` — MIT license.

## Data

- Source: UCI Machine Learning Repository (Driving Coupons) collected via Amazon Mechanical Turk.
- Label: `Y` indicates coupon acceptance (1 = accept now or later, 0 = reject).
- High-level columns (examples):
  - User attributes: `gender`, `age`, `maritalStatus`, `has_children`, `education`, `occupation`, `income`.
  - Contextual attributes: `destination`, `weather`, `temperature`, `time`, `passanger`, `direction_same`, `direction_opp`.
  - Coupon attributes: `coupon`, `expiration`, proximity indicators `toCoupon_GEQ5min`, `toCoupon_GEQ15min`, `toCoupon_GEQ25min`.
  - Outcome: `Y`.
- Missingness (from notebook exploratory step): substantial missingness in `car` (~99%) and small amounts across several frequency columns (`Bar`, `CoffeeHouse`, `CarryAway`, `RestaurantLessThan20`, `Restaurant20To50`). The notebook discusses dropping `car` and handling remaining gaps appropriately.

## Getting Started

### Prerequisites

- Python 3.9+
- Recommended packages: `pandas`, `numpy`, `matplotlib`, `seaborn`, `jupyter`

### Setup

1. Create and activate a virtual environment (optional but recommended):
   - macOS/Linux:
     ```bash
     python3 -m venv .venv
     source .venv/bin/activate
     ```
   - Windows (PowerShell):
     ```bash
     python -m venv .venv
     .\.venv\Scripts\Activate.ps1
     ```
2. Install dependencies:
   ```bash
   pip install pandas numpy matplotlib seaborn jupyter
   ```

## Running the Analysis

1. Launch Jupyter:
   ```bash
   jupyter notebook
   ```
2. Open `prompt.ipynb`.
3. Run cells sequentially. Early cells load `data/coupons.csv`, assess missingness, and show dataset info. Subsequent cells explore acceptance rates across coupon types and user/context attributes.

## Outputs & Visualizations

- The notebook produces exploratory tables and plots (via `matplotlib`/`seaborn`) to compare acceptance behavior by coupon type, time of day, passenger, weather, and more.
- Save or export figures as needed; you can add them to `images/` for documentation.

## Notes on Reproducibility

- Ensure `data/coupons.csv` exists at `data/` relative to the notebook root.
- If running in a hosted environment, upload the `data/` folder or adjust the file path accordingly.

## License

This project is licensed under the MIT License — see `LICENSE` for details.

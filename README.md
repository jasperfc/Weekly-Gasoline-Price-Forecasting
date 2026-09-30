# Weekly Gasoline Price Forecasting

> A comparative study of machine-learning methods for forecasting weekly U.S. gasoline prices.

**CSCI 567 Final Project**<br>
Simou Chen · Khalid Ali · Mario Prado · Jasper Fan-Chiang

---

## Overview

This project evaluates statistical, tree-based, and neural-network models for **1-week** and **4-week** gasoline price forecasting. It also examines how well those models perform across regions, volatile market periods, and previously unseen economic conditions.

### Models

`Naive Baseline` · `Linear Regression` · `Ridge` · `Lasso` · `Random Forest` · `XGBoost` · `MLP` · `LSTM` · `GRU`

### Key analyses

- Regional performance across five U.S. PADD regions
- Price shocks during Katrina, the 2008 crisis, the 2014–16 oil crash, and COVID-19
- Concept drift on updated 2022–2026 EIA data
- Residual bias, autocorrelation, heteroscedasticity, and Q–Q diagnostics
- Stable-versus-volatile regime performance
- Unified permutation feature importance across model families
- Cross-region generalization and transferability

## Project layout

```text
CSCI567_FinalProject/
├── data/          Raw and processed gasoline-price data
├── notebooks/     Data preparation, modeling, and analysis notebooks
├── src/           Shared data and evaluation utilities
├── results/       Saved model metrics and predictions
├── outputs/       Final figures, tables, and summary JSON files
├── report/        Draft report and supporting images
├── PLAN.md        Project plan and task division
└── README.md
```

## Notebook guide

| Notebook | Purpose | Environment |
|---|---|---|
| `01_data_cleaning_and_eda.ipynb` | Clean data, engineer features, and create chronological splits | Local |
| `02_baseline_and_linear_models.ipynb` | Baseline, Linear, Ridge, and Lasso models | Local |
| `03_tree_based_models.ipynb` | Random Forest and XGBoost with time-series tuning | Local |
| `04_neural_network_models.ipynb` | MLP, LSTM, and GRU experiments | Colab + GPU |
| `05_model_comparison_and_analysis.ipynb` | Compare models, horizons, volatility, and errors | Local |
| `06_extended_analysis.ipynb` | Regional, geopolitical-event, and concept-drift analysis | Local |
| `06b_extended_analysis_lstm_colab.ipynb` | Optional LSTM extension for regional and drift analysis | Colab + GPU |
| `07_final_analysis.ipynb` | Residual diagnostics, regimes, feature importance, and transferability | Colab + GPU |

## Quick start

### 1. Install dependencies

```bash
pip install -r Requirements.txt
```

> On macOS, XGBoost may also require OpenMP: `brew install libomp`.

### 2. Run the local workflow

```bash
cd notebooks
jupyter notebook
```

Run the local notebooks in this order:

```text
01 → 02 → 03 → 05 → 06
```

### 3. Run the neural-network notebook

Open `04_neural_network_models.ipynb` in Google Colab, select a **T4 GPU**, and run all cells. Copy the generated result JSON files into `results/`, then rerun notebook `05` locally.

### 4. Run the final analysis

For `07_final_analysis.ipynb`, upload:

- `results.zip`
- `PET_PRI_GND_DCUS_NUS_W.csv`
- All five regional XLS files
- `national_allgrades_updated.xls`

The notebook produces `final_analysis_outputs.zip`. Extract it into the project root to populate `outputs/sec1` through `outputs/sec4`.

## Data

The project uses weekly retail gasoline-price data from the **U.S. Energy Information Administration (EIA)**:

- National gasoline and diesel prices, 1995–2021
- Updated national gasoline prices through April 2026
- Regular gasoline prices for five PADD regions, 1992–2026

Raw files are kept in `data/raw/`; notebook `01` generates processed datasets in `data/cleaned/`.

## Outputs

| Folder | Contents |
|---|---|
| `outputs/sec1/` | Residual and error diagnostics |
| `outputs/sec2/` | Stable-versus-volatile regime analysis |
| `outputs/sec3/` | Cross-model feature importance |
| `outputs/sec4/` | Cross-region generalization |

## Tech stack

Python · pandas · NumPy · scikit-learn · XGBoost · PyTorch · statsmodels · Matplotlib · Seaborn · Jupyter

---

Data source: [U.S. Energy Information Administration](https://www.eia.gov/petroleum/gasdiesel/)

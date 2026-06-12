# Formative 1 — Principal Component Analysis
**Group:** 58  
**Members:** Gilbert Muramirabagabo · Kevine Uwisanga  

---

## Overview

This project implements Principal Component Analysis (PCA) **from scratch using NumPy only** on an African CO₂ emissions dataset. The goal is to reduce a 16-feature matrix to a lower-dimensional space while retaining as much variance as possible, and to interpret what is gained and lost in that reduction.

---

## Dataset

**Source:** African CO₂ emissions records across multiple countries and years  
**Shape:** 1 134 rows × 20 columns (16 numeric features used)  
**Non-numeric columns:** Country, Sub-Region, Code, Year (columns 0–3) — dropped before PCA  
**Missing values:** 1 013 NaN entries in the raw numeric matrix, imputed with column means  

**Features used (16):**
Population, GDP per capita (USD), GDP per capita PPP (USD), Area (Km²),
Transportation, Total CO₂ incl LUCF, Total CO₂ excl LUCF, Other Fuel Combustion,
Manufacturing/Construction, Land-Use Change & Forestry, Industrial Processes,
Fugitive Emissions, Energy, Electricity/Heat, Bunker Fuels, Building

---

## Repository Structure

```
Principle_Component_Analysis/
│
├── PCA_Formative_2_Group_58.ipynb   # Main notebook (all outputs visible)
├── co2 Emission Africa.csv          # Dataset
└── README.md                        # This file
```

---

## Implementation Steps

| Step | Description |
|------|-------------|
| 1 | Load CSV, isolate 16 numeric columns, report missing values |
| 2 | Impute NaNs with column means (NumPy `nanmean`) |
| 3 | Standardize: z = (x − μ) / σ (population std, ddof=0) |
| 4 | Compute covariance matrix: Cᵀ · C / (n − 1) |
| 5 | Eigendecomposition via `np.linalg.eigh` |
| 6 | Sort eigenvalues descending; compute explained variance ratios |
| 7 | Select components dynamically at 90% cumulative variance threshold → **5 PCs** |
| 8 | Project standardized data onto top-5 eigenvectors (1 134 × 16 → 1 134 × 5) |
| 9 | Visualize before PCA (Population vs GDP per capita) and after PCA (PC1 vs PC2), coloured by Sub-Region |

---

## Results

| PC | Variance Explained | Cumulative |
|----|--------------------|------------|
| 1  | 54.38 % | 54.38 % |
| 2  | 14.34 % | 68.73 % |
| 3  |  9.90 % | 78.63 % |
| 4  |  8.69 % | 87.32 % |
| **5**  |  **4.16 %** | **91.49 %** |
| 6  |  3.43 % | 94.92 % |

**5 components retained → 91.49 % of total variance preserved.**

---

## Key Findings

**Why 5 components?**  
5 is the smallest number of principal components whose cumulative explained variance reaches the 90 % threshold. The trade-off is compactness vs. completeness: we accept losing ~8.5 % of variance, mainly minor country-specific variation in exchange for a much simpler 5-dimensional representation that is faster to compute on and easier to visualise.

**What is lost?**  
PC1 acts as an economic-activity / population-pressure / total-emissions "size" axis. The top 5 PCs preserve large-scale regional structure well. What is discarded are the finer sectoral distinctions: a country whose emissions are driven primarily by land-use change rather than energy, or one with an atypical fugitive-emissions profile, may appear identical to its neighbours in the reduced space — nuances that matter for climate policy analysis.

---

## Libraries Used

| Library | Purpose |
|---------|---------|
| `numpy` | All numerical computation (standardization, covariance, eigendecomposition, projection) |
| `matplotlib` | Visualizations only |

> No `sklearn` or other ML libraries were used anywhere in this project.

---

## How to Run

1. Open `PCA_Formative_2_Group_58.ipynb` in Google Colab  
2. Upload `co2 Emission Africa.csv` to `/content/` (or mount Drive)  
3. Run all cells top to bottom — all outputs are pre-saved in the notebook  

---

## Task Contributions

See `task_sheet.pdf` for the full contribution and meeting attendance log.

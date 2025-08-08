# WeatherAUS Rainfall — Regression Analysis

Predicting **daily rainfall amount (mm)** in Australia using classic linear modeling techniques on the well-known *weatherAUS* dataset. This repo contains a single, end-to-end Jupyter notebook that walks through data cleaning, feature selection, model building, evaluation, and robustness checks.

> Core topics: multivariate linear regression (closed-form), polynomial regression and over/under-fitting, probabilistic linear regression (MLE), and ridge (L2) regularization.

---

## Repository structure

- ├── main.ipynb # end-to-end analysis & modeling workflow
- ├── weatherAUS.csv # dataset used in this project (local copy)
- └── scenario.pdf # short problem statement / context

---

## Dataset

- **Source**: widely used *Rain in Australia* (*weatherAUS*) dataset with daily observations across stations in Australia.
- **Target**: `Rainfall` (mm) — a **regression** task.
- **Features**: the notebook shows a compact set of meteorological variables (e.g., temperature, humidity, pressure, wind, cloud cover, and the “rain today” flag). Exact selections and encodings are documented where they are used in the notebook.
- **Missing values & outliers**: handled during preprocessing; see the “EDA/Preprocessing” section in `main.ipynb`.

---

## Methods & Experiments

### 1) Multivariate Linear Regression (OLS)
- Explicit design matrix (including bias term) and closed-form **Normal Equation** solution.
- Metrics: Train/Test **MSE**, residual analysis, predicted vs. actual scatter.

### 2) Polynomial Regression (1D study)
- Univariate polynomial fits on a single strong predictor (degrees like 2/3/5).
- Illustrates under- and over-fitting behavior; sensitivity to outliers is discussed/visualized.

### 3) Probabilistic Linear Regression (MLE)
- Derives the Gaussian-noise **MLE** and shows its equivalence to least squares.
- Computes (log-)likelihood on train/test and examines parameter stability under injected label noise.

### 4) Ridge Regression (L2)
- Fits ridge models across several λ values to demonstrate **coefficient shrinkage**.
- Compares generalization via Train/Test **MSE** and plots weight magnitudes vs. λ.

> The notebook includes simple ablations (e.g., dropping a feature or adding a noise feature) to sanity-check modeling choices.

---

## Results (high-level overview)

- **Linear baseline**: provides a reasonable fit on the selected features (see scatter/residual plots).
- **Polynomial**: moderate degrees improve flexibility; higher degrees can overfit and amplify outliers.
- **Probabilistic view**: as synthetic label noise increases, parameter variance rises, confirming the MLE/OLS intuition.
- **Ridge**: increasing λ shrinks coefficients and often improves test MSE vs. unregularized OLS (depending on λ and feature set).

> For exact metrics (MSE, likelihoods, coefficients) and figures, see the corresponding sections inside `main.ipynb`.

---

## Getting started

### Quick run
```bash
# 1) Clone
git clone https://github.com/Mahyar-mhn/WeatherAUS_Rainfall_Regression_Analysis.git
cd WeatherAUS_Rainfall_Regression_Analysis

# 2) (Optional) create a virtual environment
python -m venv .venv
# Windows: .venv\Scripts\activate
# macOS/Linux:
source .venv/bin/activate

# 3) Install minimal dependencies
pip install jupyter numpy pandas matplotlib

# 4) Launch the analysis
jupyter notebook main.ipynb

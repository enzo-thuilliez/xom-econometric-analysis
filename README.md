# ExxonMobil (XOM) — Econometric Analysis

A quantitative study of nearly **40 years of ExxonMobil (XOM) return data**, combining descriptive financial econometrics, GARCH volatility modelling, and factor-based asset pricing. The full analysis is implemented in Python and documented in a LaTeX report.

---

## Overview

| Item | Details |
|------|---------|
| **Asset** | ExxonMobil Corporation (XOM, NYSE) |
| **Sample** | December 1985 – December 2024 |
| **Observations** | ~9,828 daily / 468 monthly |
| **Language** | Python 3 |
| **Key libraries** | `yfinance`, `pandas`, `numpy`, `statsmodels`, `arch`, `matplotlib`, `scipy` |

---

## What's Inside

### Stylized Facts
- Computation of log-returns at daily, monthly, and annual frequencies
- Descriptive statistics: skewness, kurtosis, Jarque-Bera, Lilliefors normality tests
- Rolling moments (252-day window) to capture time-varying skewness and kurtosis
- Aggregational Gaussianity: histograms and Q–Q plots across frequencies
- Autocorrelation analysis (ACF of returns and squared returns)
- Formal tests: Ljung-Box and ARCH-LM for volatility clustering
- Leverage effect analysis via cross-correlation between returns and squared returns

### Asset Pricing
- **CAPM** (market model) — OLS estimation on monthly excess returns
- **Fama-French Three-Factor Model** (Mkt-RF, SMB, HML) — OLS estimation
- Model comparison: R², alpha significance, factor loadings
- Factor data sourced from the [Ken French Data Library](https://mba.tuck.dartmouth.edu/pages/faculty/ken.french/data_library.html)

### GARCH Extension
- GARCH(1,1) estimation on daily returns (in % form)
- Conditional volatility plot with crisis annotation (1987, 2000, 2008, 2020)
- 1-day-ahead conditional Value-at-Risk (VaR) at the 95% confidence level
- VaR backtesting with empirical coverage rate (~4.57%, expected 5%)

---

## Key Results

| Model | R² | Alpha (p-value) |
|-------|----|-----------------|
| CAPM  | 0.246 | 0.329 (p = 0.16) |
| Fama-French FF3 | 0.339 | 0.198 (p = 0.37) |

- **Market beta**: ~0.63 (CAPM) → 0.70 (FF3)
- **Value tilt**: β_HML = 0.531 (p < 0.001) — consistent with XOM's capital-intensive profile
- **GARCH persistence**: α + β ≈ 0.988 — high volatility persistence
- **No leverage effect** detected (correlation returns/volatility ≈ 0.01)

---

## Repository Structure

```
xom-econometric-analysis/
│
├── main.ipynb          # Full analysis notebook (end-to-end, reproducible)
├── report.tex          # LaTeX report source│
└── README.md
```

> **Note:** The notebook downloads XOM price data automatically from Yahoo Finance via `yfinance`. You only need to provide the Fama-French monthly factors CSV (available from the Ken French Data Library).

---


## CV Highlight

> **Econometric Analysis of ExxonMobil (XOM) — 1985–2024**
> Leveraged Python to analyze nearly 40 years of daily return data, quantifying volatility clustering and leptokurtosis via Jarque-Bera/Lilliefors/ARCH-LM tests. Estimated CAPM and Fama-French 3-Factor models on monthly excess returns; FF3 R² = 0.34 with a significant value tilt (β_HML = 0.53). Extended the analysis with a GARCH(1,1) model for conditional VaR estimation, achieving 4.57% empirical coverage vs. 5% theoretical.

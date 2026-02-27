# 📈 Portfolio Risk Optimizer — Python

![Language](https://img.shields.io/badge/language-Python%203.10-blue?style=flat-square)
![Build](https://img.shields.io/badge/build-passing-brightgreen?style=flat-square)
![License](https://img.shields.io/badge/license-MIT-lightgrey?style=flat-square)
![Domain](https://img.shields.io/badge/domain-Risk%20Analytics-red?style=flat-square)

> A Python toolkit for portfolio construction and risk analysis. Implements Modern Portfolio Theory, Black-Litterman, and coherent risk measures (VaR / CVaR) on real market data.

---

## 🎯 Overview

This project was built to explore the mathematics behind portfolio optimization — going beyond textbook theory and implementing everything on real historical return data. The goal was to understand *quantitative risk management* from the ground up, using only scientific Python (NumPy, pandas, cvxpy).

```
  Historical Returns (pandas)
          │
          ▼
  Covariance Estimation ──► Shrinkage (Ledoit-Wolf)
          │
          ▼
  Optimization (cvxpy) ──► Max Sharpe / Min Volatility / Risk Parity
          │
          ▼
  Risk Metrics ──► VaR (95%, 99%), CVaR, Max Drawdown, Beta
          │
          ▼
  Efficient Frontier Plot (matplotlib)
```

---

## 🧠 Features

| Feature | Description |
|---|---|
| Efficient Frontier | Mean-variance optimization with constraints |
| Black-Litterman | Bayesian integration of investor views |
| Covariance Shrinkage | Ledoit-Wolf estimator for ill-conditioned matrices |
| VaR / CVaR | Historical and parametric methods (95%, 99%) |
| Risk Parity | Equal risk contribution across assets |
| Backtesting | Walk-forward portfolio performance analysis |

---

## 🚀 Getting Started

### Prerequisites

```bash
Python >= 3.10
pip install numpy pandas cvxpy matplotlib scipy
```

### Installation & Run

```bash
git clone https://github.com/elouafi-abderrahmane-2002/PyPortfolioOpt.git
cd PyPortfolioOpt
pip install -r requirements.txt
python main.py
```

### Example Usage

```python
from optimizer import EfficientFrontier
from risk import RiskMetrics

# Load returns and optimize
ef = EfficientFrontier(returns_df, risk_free_rate=0.04)
weights = ef.max_sharpe()
print(ef.portfolio_performance())
# Expected return: 12.4% | Volatility: 9.1% | Sharpe: 1.35

# Compute risk metrics
rm = RiskMetrics(returns_df, weights)
print(f"VaR (95%):  {rm.var(confidence=0.95):.2%}")   # -2.31%
print(f"CVaR (95%): {rm.cvar(confidence=0.95):.2%}")  # -3.57%
```

---

## 📊 Sample Output

```
Portfolio Optimization Results
══════════════════════════════════════════
  Assets          :  AAPL, MSFT, JPM, GLD
  Optimization    :  Maximum Sharpe Ratio
──────────────────────────────────────────
  Expected Return :  12.4%
  Volatility      :  9.1%
  Sharpe Ratio    :  1.35
──────────────────────────────────────────
  VaR  (95%)      : -2.31%   [daily]
  CVaR (95%)      : -3.57%   [daily]
  Max Drawdown    : -14.2%   [2023 period]
══════════════════════════════════════════
```

---

## 📐 Project Structure

```
PyPortfolioOpt/
├── optimizer/
│   ├── efficient_frontier.py
│   ├── black_litterman.py
│   └── risk_parity.py
├── risk/
│   ├── metrics.py         # VaR, CVaR, Drawdown
│   └── covariance.py      # Shrinkage estimators
├── data/
│   └── fetch_prices.py    # Yahoo Finance loader
├── tests/
│   └── test_optimizer.py
├── notebooks/
│   └── exploration.ipynb
├── main.py
└── requirements.txt
```

---

## 📚 What I Learned

- **Why covariance matrices break** — with N assets and T observations, if T < N the sample covariance is singular. Ledoit-Wolf shrinkage fixes this in a mathematically principled way. This was the hardest concept to internalize.
- **CVaR vs VaR** — VaR tells you the threshold; CVaR tells you the *expected loss beyond that threshold*. For risk management, CVaR is almost always the better metric because it's coherent (subadditive).
- **Convex optimization in practice** — formulating the portfolio problem as a quadratic program and solving it with cvxpy taught me how powerful and concise disciplined convex optimization can be.
- **Data pitfalls** — survivorship bias, look-ahead bias, and how to properly structure a walk-forward backtest without leaking future information.

---

## 👤 Author

**Abderrahmane Elouafi**
Final-year Engineering Student — Big Data & Cloud Computing, ENSET Mohammedia
[LinkedIn](https://www.linkedin.com/in/abderrahmane-elouafi-43226736b/) · [Portfolio](https://my-first-porfolio-six.vercel.app/) · [GitHub](https://github.com/elouafi-abderrahmane-2002)

---

*Numbers don't lie — but you have to know which numbers to trust.*

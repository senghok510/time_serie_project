# Time Series Gold

This repository contains two exploratory Jupyter notebooks focused on financial time-series modeling:

- `main.ipynb`: gold futures (`GC=F`) return and volatility analysis using ARIMA and GARCH.
- `couple.ipynb`: dependence modeling and pairs-trading research on `VIX` and `RVX` using fitted marginals and copulas.

The project is notebook-first. There is no packaged Python module or CLI entry point in the repository at the moment.

## Repository Contents

- `main.ipynb`
  Studies daily gold futures data downloaded from Yahoo Finance.
  The notebook:
  - downloads `GC=F` data from January 1, 2025 to April 1, 2026
  - computes log-prices and log-returns
  - checks stationarity with the ADF test
  - inspects autocorrelation with ACF, PACF, and Ljung-Box tests
  - fits an `ARIMA(1,0,1)` mean model on returns
  - checks residual normality with Jarque-Bera
  - tests for ARCH effects
  - fits `GARCH(1,1)` models with normal and Student-t errors
  - compares volatility forecasts against a realized-volatility proxy using the Garman-Klass estimator

- `couple.ipynb`
  Studies the joint behavior of `VIX` and `RVX` from FRED and builds a rolling copula-based trading signal.
  The notebook:
  - downloads `VIXCLS` and `RVXCLS` from FRED
  - computes log-returns
  - fits marginal distributions for each series
  - transforms returns to uniform pseudo-observations
  - compares several copula families by likelihood, AIC, and BIC
  - generates rolling conditional probabilities
  - applies a simple pairs-trading strategy with open and close thresholds
  - reports strategy metrics such as total return, APR, Sharpe ratio, and max drawdown

## Data Sources

- Yahoo Finance via `yfinance` for gold futures (`GC=F`)
- FRED via `pandas_datareader` for:
  - `VIXCLS`
  - `RVXCLS`

Both notebooks pull data at runtime. No raw datasets are stored in this repository.

## Main Methods Used

- Log-return transformation
- Stationarity testing: `ADF`, `KPSS`
- Serial dependence diagnostics: `ACF`, `PACF`, `Ljung-Box`
- Mean modeling: `ARIMA`
- Volatility modeling: `GARCH(1,1)`
- Distribution fitting with `AIC`, `BIC`, and `KS` diagnostics
- Copula family selection and rolling dependence-based trading signals

## Environment

The notebooks were created with a Python 3 kernel. Dependencies are listed in `requirements.txt`.

```bash
pip install -r requirements.txt
```

Notes:

- `main.ipynb` uses `yfinance`, `statsmodels`, `arch`, and `scikit-learn`.
- `couple.ipynb` uses `pandas-datareader` and a `copulas` package or module.
- This repository does not currently include a local `copulas.py`, so `couple.ipynb` depends on an external `copulas` implementation being available in your environment.

## How To Run

1. Create and activate a Python environment.
2. Install the dependencies from `requirements.txt`.
3. Start Jupyter:

```bash
jupyter notebook
```

4. Open either:
   - `main.ipynb`
   - `couple.ipynb`

Because the notebooks fetch live market data, results can differ from one run to another if the data providers revise or extend the series.

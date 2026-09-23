# Ethereum (ETH-USD) Time Series Analysis & Forecasting

*Group project — built with Mandar Tarmale, MSc Big Data Analytics coursework.*

A comparison of five forecasting techniques on 5 years of daily Ethereum (ETH-USD) price data (Sep 2019 – Sep 2024), to identify which approach best captures the coin's volatile price behavior.

## Approach

- Pulled 5 years of daily ETH-USD data via `yfinance`
- Tested stationarity with the **Augmented Dickey-Fuller (ADF) test**, applied first-order and log differencing to stabilize the series
- Used **ACF/PACF plots** to identify AR and MA lag parameters
- Ran a **multiplicative seasonal decomposition** to separate trend, seasonality, and residual noise
- Split data 70:30 into train/test sets
- Used `auto_arima` (pmdarima) on the log-transformed training series for ARIMA order selection — it settled on ARIMA(1,1,1)
- Trained and scored **four forecasting models**: SARIMA, Holt's Winter Exponential Smoothing, LSTM (neural network), and Prophet
- Evaluated each model with **RMSE** on the held-out test set

## Results

| Model | RMSE |
|---|---|
| **LSTM** | **135.82** ✅ Best performer |
| SARIMA | 1031.44 |
| Holt's Winter | 1040.08 |
| Prophet | 1594.13 |

**LSTM significantly outperformed the classical statistical models** — roughly 7.6× lower error than the next best — suggesting Ethereum's price behavior contains complex, non-linear patterns that a neural network captures far better than ARIMA-family or exponential smoothing approaches.

SARIMA and Holt's Winter landed close together (1031 vs. 1040). **Prophet was the weakest of the four** at 1594.13: its additive trend-plus-seasonality structure is a poor match for a series whose seasonal component is weak and whose volatility dominates, which the seasonal decomposition had already hinted at.

> **Note on scope:** ARIMA appears in the analysis for parameter selection only. `auto_arima` was used to identify the best (p,d,q) order, but no separate ARIMA forecast was generated, so it carries no RMSE in the comparison above.

## Files

- [`notebook/ETH_USD_Time_Series_Forecasting.ipynb`](./notebook/ETH_USD_Time_Series_Forecasting.ipynb) — full analysis, from data pull through model comparison

## Tech Stack

Python · pandas · statsmodels · pmdarima · scikit-learn · Prophet · yfinance

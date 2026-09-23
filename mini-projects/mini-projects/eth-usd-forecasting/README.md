# Ethereum (ETH-USD) Time Series Analysis & Forecasting

*Group project — built with Mandar Tarmale, MSc Big Data Analytics coursework.*

A comparison of five forecasting techniques on 5 years of daily Ethereum (ETH-USD) price data (Sep 2019 – Sep 2024), to identify which approach best captures the coin's volatile price behavior.

## Approach

- Pulled 5 years of daily ETH-USD data via `yfinance`
- Tested stationarity with the **Augmented Dickey-Fuller (ADF) test**, applied first-order and log differencing to stabilize the series
- Used **ACF/PACF plots** to identify AR and MA lag parameters
- Ran a **multiplicative seasonal decomposition** to separate trend, seasonality, and residual noise
- Split data 70:30 into train/test sets
- Trained and compared **five models**: ARIMA, SARIMA, Holt's Winter Exponential Smoothing, LSTM (neural network), and Prophet
- Evaluated each model with **RMSE** on the held-out test set

## Results

| Model | RMSE |
|---|---|
| **LSTM** | **156.43** ✅ Best performer |
| SARIMA | 1067.55 |
| Holt's Winter | 1197.64 |
| Prophet | 1594.13 |

**LSTM significantly outperformed the classical statistical models**, suggesting Ethereum's price behavior contains complex, non-linear patterns that a neural network captures far better than ARIMA-family or exponential smoothing approaches. Prophet, while easier to interpret and faster to run, traded accuracy for that simplicity.

## Files

- [`notebook/ETH_USD_Time_Series_Forecasting.ipynb`](./notebook/ETH_USD_Time_Series_Forecasting.ipynb) — full analysis, from data pull through model comparison

## Tech Stack

Python · pandas · statsmodels · pmdarima · scikit-learn · Prophet · yfinance

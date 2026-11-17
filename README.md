# Google stock price forecast with Prophet

> Course assignment from 2023, kept as it was written. The notes under "Reading the result" were added in November 2026.

Forecasts Google's closing price 100 days ahead with Prophet, on daily prices from January 2013
to December 2017.

## Method

1. Put the trading days on a daily calendar and interpolate weekends and holidays.
2. Decompose the series and test for stationarity (ADF p = 0.93: not stationary).
3. Grid-search 30 combinations of changepoint scale, number of changepoints and seasonality scale,
   scoring each on the last 50 days.
4. Refit and forecast 100 days.

## Result

Error on the last 50 days ranges from 3.5% to 5.4% MAPE across the grid. The best setting
(changepoint scale 0.1, 100 changepoints, seasonality scale 10) scores **3.5%**.

## Reading the result

- **There is no baseline.** For a stock price, "tomorrow equals today" is hard to beat, and the
  notebook does not compare against it. Without that number 3.5% cannot be called good.
- The setting was chosen on the same 50 days that the error is reported on.
- Prophet fits a trend and yearly seasonality. Prices have neither in a form that persists, so
  the 100-day forecast is an extrapolated trend line with a wide band.
- The brief asked for Bayesian optimisation; the notebook uses a grid.

## Newer work on the same topic

- [demand-forecasting-backtest](https://github.com/faiqrasulov/demand-forecasting-backtest): a 12-origin rolling backtest against a seasonal-naive baseline, with measured interval coverage.

## Files

| File | Content |
|---|---|
| `Google Stock Price Prediction.ipynb` | Analysis (uses `fbprophet`, now published as `prophet`) |
| `Google Stock Price Prediction.html` | Rendered copy |
| `google-data.csv` | Daily prices |
| `About.txt` | Original brief |

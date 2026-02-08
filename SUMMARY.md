# Auquan Tutorials - Repository Summary

A collection of 20 Jupyter notebooks providing educational tutorials on quantitative finance, statistical analysis, and algorithmic trading strategies. The tutorials draw from Quantstart and Quantopian Lecture Series content and use the [Auquan Toolbox](https://github.com/Auquan/auquan-toolbox-python) for backtesting.

---

## Statistical Foundations

| Notebook | Description |
|----------|-------------|
| **Random Variables** | Introduction to random variables, probability distributions, and discrete vs continuous variables. |
| **Expected Value and Standard Deviation** | Covers arithmetic/geometric/harmonic means, median, mode, variance, standard deviation, and volatility. |
| **Covariance, Correlation and Confidence Intervals** | Explains covariance, correlation, confidence intervals, t-tests, and Newey-West corrections for autocorrelated data. |
| **Integration, Cointegration, and Stationarity** | Orders of integration I(0)/I(1), Augmented Dickey-Fuller test, and cointegration tests for pairs trading. |

## Time Series Analysis (4-part series)

| Notebook | Description |
|----------|-------------|
| **Part 1** | Stationarity, autocorrelation, white noise, and random walks. |
| **Part 2** | Autoregressive (AR) and Moving Average (MA) models with ACF/PACF analysis. |
| **Part 3** | ARMA and ARIMA models for forecasting. |
| **Part 4** | Conditional heteroskedasticity, ARCH, and GARCH models for volatility modeling. |

## Trading Strategies

| Notebook | Description |
|----------|-------------|
| **Mean Reversion** | Single-stock, portfolio-based, and pairs-based mean reversion using z-score signals. |
| **Momentum Strategies** | Momentum vs mean reversion, autocorrelation testing, entry/exit signals, and cross-sectional momentum. |
| **Measuring Momentum** | Moving average crossovers/ribbons, distance metrics, correlation metrics, and physics-based momentum measures. |
| **Pairs Trading** | Finding cointegrated pairs, computing z-scores, generating signals, and backtesting with rolling statistics. |
| **Long-Short Strategies using Ranking** | Market-neutral long-short equity strategies based on stock ranking schemes. |
| **ARIMA + GARCH to model SPX returns** | Combined ARIMA/GARCH model to predict and trade S&P 500 daily returns. |

## Machine Learning for Trading

| Notebook | Description |
|----------|-------------|
| **Introduction to ML for Trading** | End-to-end ML workflow: problem setup, feature engineering, model training (ExtraTreesRegressor), and backtesting. |
| **Simple ML Strategies to generate Trading Signal** | Applying ML to generate trading signals with focus on avoiding common pitfalls. |

## Model Validation and Pitfalls

| Notebook | Description |
|----------|-------------|
| **Overfitting** | Curve fitting examples, rolling window optimization pitfalls, cross-validation, and AIC. |
| **Trading Strategy Model Selection Pitfalls** | Choosing variables, functional forms, exclusion of important variables, and model consistency. |

## Practical Backtests

| Notebook | Description |
|----------|-------------|
| **momentum_backtest_losing_money** | Momentum/mean reversion backtest demonstrating a losing strategy (parameter sensitivity). |
| **momentum_backtest_making_money** | Momentum/mean reversion backtest demonstrating a profitable strategy. |

---

## Key Libraries Used

- **Statistical Analysis**: numpy, pandas, scipy, statsmodels
- **Visualization**: matplotlib, seaborn
- **Machine Learning**: scikit-learn
- **Time Series / Volatility**: statsmodels.tsa, arch
- **Backtesting**: Auquan Toolbox (backtester, dataloader)
- **Data Sources**: Yahoo Finance (YahooStockDataSource), CSV files

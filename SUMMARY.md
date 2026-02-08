# Auquan Tutorials - Repository Summary

A collection of 20 Jupyter notebooks providing educational tutorials on quantitative finance, statistical analysis, and algorithmic trading strategies. The tutorials draw from Quantstart and Quantopian Lecture Series content and use the [Auquan Toolbox](https://github.com/Auquan/auquan-toolbox-python) for backtesting.

---

## Statistical Foundations

### Random Variables
Introduction to random variables and probability distributions. Covers discrete and continuous random variables, cumulative distribution functions (CDF), and probability density functions (PDF). Uses theoretical examples (dice rolls, coin flips) to build intuition before connecting to stock price modeling concepts.

### Expected Value and Standard Deviation
Explores measures of central tendency — arithmetic mean, weighted mean, median, mode, geometric mean, and harmonic mean — and when each is appropriate. Introduces variance, standard deviation, and mean absolute deviation as measures of dispersion. Demonstrates that geometric mean is the correct measure for average returns and that volatility is the annualized standard deviation.

### Covariance, Correlation and Confidence Intervals
Explains covariance and correlation between random variables using real stock data (AAPL, LRCX, MSFT, SPX from 2014-2017). Covers confidence intervals via t-distributions, Spearman rank correlation, and the Ljung-Box test for autocorrelation. Demonstrates that rolling correlations between stocks can change sign over time, and introduces Newey-West corrections when standard error assumptions are violated by autocorrelated data.

### Integration, Cointegration, and Stationarity
Defines orders of integration I(0) and I(1) and demonstrates the Augmented Dickey-Fuller (ADF) test for stationarity. Shows that price series are typically non-stationary I(1) while returns are stationary I(0). Tests cointegration between MSFT/ADBE and SPX/AAPL (2007-2017) using `statsmodels.coint()`, establishing the statistical foundation for pairs trading. Emphasizes the importance of out-of-sample validation for cointegration relationships.

---

## Time Series Analysis (4-part series)

### Part 1 — Stationarity, Autocorrelation, White Noise and Random Walks
Introduces stationarity requirements for time series modeling and demonstrates ACF/PACF plots for identifying serial correlation. Compares white noise processes with random walks, showing that first-differencing a random walk produces white noise. Uses S&P 500, DOW, and MSFT data (2014-2017) and QQ plots to show that stock returns exhibit heavy tails (non-normal).

### Part 2 — AR and MA Models
Covers Autoregressive AR(p) and Moving Average MA(q) models. Explains how to use PACF to determine AR order and ACF for MA order. Fits models to S&P 500 and AAPL log returns, finding that financial data often requires high-order models (e.g., AR(16), MA(3)). Uses AIC for model selection and the Jarque-Bera test to assess residual normality.

### Part 3 — ARMA and ARIMA Models
Combines AR and MA into ARMA(p,q) and adds differencing for ARIMA(p,d,q). Performs a grid search over parameters using AIC, identifying ARIMA(3,0,2) as the best model for S&P 500 log returns (2010-2017). Demonstrates 21-day-ahead forecasting with widening confidence intervals and applies the Ljung-Box test to verify that residuals are white noise. Notes that excluding volatile periods (e.g., 2008 crisis) improves model fit.

### Part 4 — ARCH and GARCH Models
Addresses volatility clustering in financial returns through ARCH(p) and GARCH(p,q) models. Defines the variance equations and demonstrates fitting via the `arch` package. Shows that combined ARIMA+GARCH modeling outperforms ARIMA alone by capturing both mean and variance dynamics. Recommends checking squared residuals for autocorrelation and using Student's t-distribution for improved fit.

---

## Trading Strategies

### Mean Reversion
Presents three approaches to mean reversion: single-stock (exposes to market risk), portfolio-based (provides market neutrality), and pairs-based (requires cointegration). Demonstrates z-score calculation `(value - mean) / std` with both cumulative and rolling statistics on PG, AAPL, HP, and MSFT (2012-2016). Trading signals are generated when z-scores cross entry/exit thresholds.

### Momentum Strategies
Contrasts momentum with mean reversion and explains how autocorrelation in returns drives momentum effects. Uses linear regression and ADF tests on AAPL (2014-2017) to identify trending behavior. Highlights that the same asset can exhibit momentum on long timeframes and mean reversion on short timeframes. Covers cross-sectional momentum for ranking stocks relative to each other.

### Measuring Momentum
Goes beyond simple moving average crossovers to introduce moving average ribbons, Hamming distance, and Spearman correlation between ribbon orderings. Develops physics-based momentum measures (p(0) through p(3)) that incorporate volume as "mass" and price velocity. Tests across 10 diverse stocks (AAPL, AIG, C, T, PG, JNJ, EOG, MET, DOW, AMGN) from 2014-2016. Warns that lookback period optimization is a major overfitting risk.

### Pairs Trading
Full implementation of a pairs trading strategy on ADBE/MSFT (2007-2017). Covers cointegration testing, z-score computation on the price ratio, and signal generation (entry at +/-1 std, exit at +/-0.5 std) using 60-90 day rolling windows. Backtests the strategy with train/validation/test splits, achieving $545k profit on test data. Discusses how window length optimization leads to overfitting and the importance of controlling for confounding market factors.

### Long-Short Strategies using Ranking
Builds a market-neutral long-short equity portfolio by ranking 32 S&P 500 stocks on 30-day momentum (2010-2017). Goes long the top quintile and short the bottom quintile with equal dollar weighting. Analyzes basket return spreads and rank-return correlations. Achieves 5.03% annual returns in the example. Discusses practical considerations: transaction costs, capital requirements (needs millions for 1000+ equities), and the high capacity scalability of ranking strategies.

### ARIMA + GARCH to Model SPX Returns
Applies the time series theory from earlier notebooks to build a complete trading strategy on the S&P 500 (2014-2017). Uses a 500-day rolling window to fit ARIMA models for return forecasts and GARCH for variance forecasts daily. Trades based on the sign of the predicted return. The combined model outperforms buy-and-hold but is computationally intensive (32 ARIMA fits per day) and does not account for transaction costs.

---

## Machine Learning for Trading

### Introduction to ML for Trading
End-to-end ML workflow applied to predicting stock-future basis spread (MQK instrument) using minute-level data. Engineers features and compares Linear Regression, Extra Trees Regressor, KNN, and SVR. Extra Trees performs best (MSE: 0.53, R^2: 0.99). Demonstrates feature correlation analysis to identify redundancy, model persistence with pickle, and backtesting that yields $1,169 PnL on test data. Emphasizes that feature selection matters more than model choice.

### Simple ML Strategies to Generate Trading Signal
Builds on the ML introduction with more rigorous feature engineering: momentum indicators, EMA features, RSI, and volume ratios. Starts with 38 features and reduces to 7 key features via correlation analysis. Compares models on the same MQK basis spread data across train/validation/test sets. Achieves test MSE of 0.07 with an ensemble of all models, demonstrating good generalization. Focuses on avoiding common pitfalls like data leakage and look-ahead bias.

---

## Model Validation and Pitfalls

### Overfitting
Illustrates overfitting through polynomial regression (showing a 9th-degree polynomial fits noise, not signal), multiple regression with irrelevant variables, and rolling window optimization. Uses PG, PEP, MCD, CVS, and DOW stocks (2014-2016) to demonstrate that optimal window lengths found on training data fail out-of-sample. Teaches the parsimony principle (fewer parameters are better), cross-validation, and AIC as defenses against overfitting.

### Trading Strategy Model Selection Pitfalls
Covers common modeling mistakes: omitted variable bias, inclusion of unnecessary variables, confounding variables (two stocks correlating through the market), and pooling different populations. Demonstrates spurious correlations between random walks on AAPL, LRCX, and S&P 500 (2013-2016), where an R^2 of 0.90 in-sample drops to 0.73 out-of-sample. Argues that economic reasoning should drive model choice and that differences (returns) should be modeled instead of levels (prices) for non-stationary series.

---

## Practical Backtests

### momentum_backtest_losing_money
Implements a basic momentum strategy on AAPL (2015-2017) using the Auquan Toolbox. Uses a 90-day moving average with 30-day and 10-day momentum indicators — goes long when momentum is positive, short when negative. Serves as an educational example of a strategy that loses money due to naive signal generation without regime detection.

### momentum_backtest_making_money
Enhances the losing strategy by adding a Hurst exponent filter. The Hurst exponent determines the regime: H > 0.5 indicates trending (trade momentum), H < 0.5 indicates mean-reverting (avoid momentum), H = 0.5 indicates a random walk. Only trades when both short-term and long-term momentum agree and the Hurst exponent confirms a trending regime. Demonstrates dramatically improved performance on the same AAPL data, illustrating the value of regime detection.

---

## Key Libraries Used

- **Statistical Analysis**: numpy, pandas, scipy, statsmodels
- **Visualization**: matplotlib, seaborn
- **Machine Learning**: scikit-learn (ExtraTreesRegressor, KNN, SVR, LinearRegression)
- **Time Series / Volatility**: statsmodels.tsa, arch
- **Backtesting**: Auquan Toolbox (backtester, dataloader)
- **Data Sources**: Yahoo Finance (YahooStockDataSource), CSV files

## Suggested Learning Path

1. **Statistics first**: Random Variables → Expected Value → Covariance/Correlation → Integration/Cointegration
2. **Time series**: Parts 1-4 (stationarity → AR/MA → ARMA/ARIMA → ARCH/GARCH)
3. **Strategies**: Mean Reversion → Momentum → Pairs Trading → Long-Short Ranking → ARIMA+GARCH
4. **ML**: Introduction to ML → Simple ML Strategies
5. **Validation**: Overfitting → Model Selection Pitfalls
6. **Practice**: Losing Backtest → Winning Backtest (compare side-by-side)

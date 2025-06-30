# Unsupervised Learning-Based Trading Strategy

This project implements a quantitative trading strategy using unsupervised learning (K-Means clustering) to identify latent market regimes across S&P 500 stocks. By combining technical indicators, factor exposures, and portfolio optimization, the strategy aims to construct monthly rebalanced portfolios that outperform the SPY benchmark.

## Overview

- **Goal**: Identify clusters of stocks with similar factor/technical profiles and exploit them to generate alpha.
- **Universe**: S&P 500 stocks
- **Frequency**: Monthly rebalancing
- **Timeframe**: 8 years (2015–2023)
- **Benchmark**: SPY ETF (Buy & Hold)

## Methodology

1. **Data Collection**
   - Pulled historical price data using `yfinance` for all S&P 500 constituents.
   - Collected Fama-French 5-factor data using `pandas_datareader`.

2. **Feature Engineering**
   - Computed technical indicators: RSI, Bollinger Bands, MACD, ATR, Garman-Klass volatility.
   - Calculated dollar volume and filtered the top 150 most liquid stocks monthly.
   - Estimated rolling betas with respect to Fama-French factors using `RollingOLS`.

3. **Clustering**
   - Applied K-Means clustering with 4 clusters using RSI-driven initial centroids.
   - Clustered stocks monthly based on engineered features and factor exposures.

4. **Portfolio Construction**
   - Selected stocks from the most promising cluster (based on RSI and returns).
   - Performed mean-variance optimization using `PyPortfolioOpt` to maximize Sharpe ratio under weight constraints.
   - Rebalanced the portfolio monthly using historical return and covariance estimates.

5. **Backtesting**
   - Constructed cumulative return time series and compared strategy performance to SPY.
   - Evaluated returns using visual plots and metrics like Sharpe Ratio.

## Key Libraries

- `pandas`, `numpy`, `matplotlib`, `scikit-learn`, `statsmodels`, `pandas-ta`, `yfinance`
- `pypfopt` for portfolio optimization

## Results

The strategy demonstrated superior cumulative returns relative to the SPY ETF benchmark over an 8-year backtest, with visually distinguishable outperformance and diversified exposure across market regimes.

![Returns Chart](path/to/chart.png) <!-- Optional: replace with actual chart path -->

## Folder Structure

```bash
.
├── Unsupervised_Learning_Trading_Strategy.py  # Main script
├── requirements.txt                           # Python dependencies
├── README.md                                  # This file

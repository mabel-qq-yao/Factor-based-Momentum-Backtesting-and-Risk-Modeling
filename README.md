# Factor-based-Momentum-Backtesting-and-Risk-Modeling
Factor-based Momentum, Backtesting and Risk Modeling

1- Historical Data Acquisition: Stock, futures, and fund prices / Financial indicators and macroeconomic data

2- Signal Calculation: 
Momentum: past N-day returns
Value: P/E, P/B, etc.
Size: market capitalization

3- Signal Grouping
Based on quantiles or thresholds
Top group → expected high returns
Bottom group → expected low returns

4- Future Return Calculation
Compute future returns for each group after the signal formation

5- Cumulative Returns & Portfolio Construction
Equal-weighted or market-cap-weighted portfolio
Compute the NAV (Net Asset Value) curve

6- Risk Metrics Calculation
Annualized volatility, maximum drawdown, VaR, CVaR

7- Statistical Significance Testing
Regression or t-test
Verify whether the signal has predictive power

8- Signal Effectiveness Evaluation
If effective → can be used to build a quantitative strategy
If not → adjust the signal or redesign the factor


keywords: 
Factor-based → Momentum、Value、Size
Momentum → signal
Backtesting → historical data
Risk Modeling → VaR、CVaR、EWMA、Volatility、MDD


import pandas as pd
import numpy as np
from scipy.stats import ttest_ind

# 取最新信号
signal = momentum.iloc[-1]

# 分组
top_quantile = 0.2
bottom_quantile = 0.2
n_top = int(top_quantile * len(signal))
n_bottom = int(bottom_quantile * len(signal))

top_group = signal.nlargest(n_top).index
bottom_group = signal.nsmallest(n_bottom).index

# 未来 20 天收益
future_returns = prices.pct_change(20).iloc[-20:]

# 计算每组平均未来收益
top_returns = future_returns[top_group].mean(axis=1)
bottom_returns = future_returns[bottom_group].mean(axis=1)

# t-test
t_stat, p_value = ttest_ind(top_returns, bottom_returns)
print(f"t-statistic: {t_stat:.3f}, p-value: {p_value:.3f}")

if p_value < 0.05:
    print("Top/Bottom group difference is statistically significant.")
else:
    print("No significant difference between groups.")


    




If effective → can be used to build a quantitative strategy

If not → adjust the signal or redesign the factor

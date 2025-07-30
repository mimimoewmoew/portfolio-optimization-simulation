# portfolio optimization simulation
# Project Overview
Project Title: Portfolio Optimization and Risk Analysis  
Database: yfinance  
This project simulates 10,000 randomly generated investment portfolios using historical data from ETFs (SPY, QQQ, TLT, GLD, SHY) and applies Modern Portfolio Theory (MPT) to identify optimal allocations.

---

## Objectives
1. **Download real market data** using 'yfinance'  
2. Calculate **annualized returns, volatility, and covariance**  
3. **Simulate portfolio combinations** with random weights  
4. Visualize the **Efficient Frontier and identify**:
  - ⭐ The Max Sharpe Ratio portfolio
  - ❌ The Minimum Volatility portfolio

---

## Efficient Frontier (Result)
<img width="930" height="590" alt="efficient_frontier" src="https://github.com/user-attachments/assets/77f0db8b-3a43-46a1-9f0f-e631af7887e5" />



---

## Key Insights

- Optimal portfolio achieved the best risk-adjusted return based on the Sharpe Ratio
- Diversifying with equities and long/short-term bonds reduced portfolio risk
- Risk-return tradeoff is clearly visualized and quantified

---

## Tools Used

- Python (Google Colab)
- 'yfinance', 'numpy', 'pandas', 'matplotlib'
- GitHub for project presentation

---

## Project Structure
**1. Data Acquisition**  
&nbsp;&nbsp;&nbsp;&nbsp;Library Used: yfinance  
&nbsp;&nbsp;&nbsp;&nbsp;Assets Selected: SPY, QQQ, TLT, GLD, SHY  
&nbsp;&nbsp;&nbsp;&nbsp;Time Period: January 2020 – July 2024  
&nbsp;&nbsp;&nbsp;&nbsp;Objective: Collect daily adjusted close prices for each asset to simulate portfolio returns
```
import yfinance as yf
tickers = ['SPY', 'QQQ', 'TLT', 'GLD', 'SHY']
raw_data = yf.download(tickers, start="2020-01-01", end="2024-07-01",auto_adjust=False)
data = raw_data['Adj Close']
data.head()
```
**2. Return and Risk Calculation**  
&nbsp;&nbsp;&nbsp;&nbsp;Daily Returns: Calculated using .pct_change()  
&nbsp;&nbsp;&nbsp;&nbsp;Annualized Return: Mean daily return × 252 trading days  
&nbsp;&nbsp;&nbsp;&nbsp;Annualized Covariance: Covariance of returns × 252  
&nbsp;&nbsp;&nbsp;&nbsp;Used to estimate expected return and volatility of portfolio
```
returns = data.pct_change().dropna()
mean_returns = returns.mean() * 252
cov_matrix = returns.cov() * 252
```
**3. Portfolio Simulation**

&nbsp;&nbsp;&nbsp;&nbsp;**Number of Portfolios**: 10,000  
&nbsp;&nbsp;&nbsp;&nbsp;**Random Weight Generation**: Each portfolio has randomly assigned asset weights summing to 1  
&nbsp;&nbsp;&nbsp;&nbsp;**Calculated Metrics**:  
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Expected Return  
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Portfolio Volatility (standard deviation)  
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Sharpe Ratio (using risk-free rate = 2%)

```
for i in range(10000):
    weights = np.random.random(len(mean_returns))
    weights /= np.sum(weights)
    portfolio_return = np.dot(weights, mean_returns)
    portfolio_stddev = np.sqrt(np.dot(weights.T, np.dot(cov_matrix, weights)))
    sharpe_ratio = (portfolio_return - risk_free_rate) / portfolio_stddev
```

**4. Optimization & Visualization**

**Identified**:
  - ⭐ Portfolio with Max Sharpe Ratio (best risk-adjusted return)  
  - ❌ Portfolio with Min Volatility (most stable)

**Visualized**:
  - Efficient Frontier (scatter plot of 10,000 portfolios)  
  - Highlighted optimal portfolios using markers for easy comparison

```
plt.scatter(results_df['Volatility'], results_df['Return'], c=results_df['Sharpe Ratio'], cmap='viridis')
plt.scatter(..., marker='*', color='r', label='Max Sharpe Ratio')
plt.scatter(..., marker='X', color='b', label='Min Volatility')
```
## About Me

I’m an undergraduate student at the University of Toronto, studying **Actuarial Science and Statistics double major**.  
This project reflects my growing interest in **investment strategy**, **risk analysis**, and **quantitative finance**.

[LinkedIn](https://www.linkedin.com/in/sylvia-wang-b089692a9/)  

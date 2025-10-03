# Portfolio Construction Strategy

This project builds and evaluates **two portfolio construction strategies** across **six portfolios** using Yahoo Finance data and a consistent out-of-sample backtest.

---

## Objectives
- Construct portfolios using both **signal-driven selection + efficient frontier** and **rebalancing-frequency** approaches.
- Compare performance with business-relevant metrics (CAGR, Vol, Sharpe, Max Drawdown).

---

## Dataset & Setup
- **Source**: Yahoo Finance via `yfinance`
- **Dataset**: Daily adjusted close prices of S&P 500 component stocks.
- **Time Period**: Data covers January 1, 2015 – December 31, 2024 (10 years).
- **Risk-free rate**: 0.023

**Feature Engineering / Signals**
- **Sharpe Ratio** — Used to rank stocks for Strategy 1
- **Beta (CAPM)** — Calculated against a benchmark to select stocks for Strategy 1

---

## Methods (Two Strategies, Six Portfolios)

### Strategy 1 — Signal-Driven Efficient Frontier (Portfolios 1–3)
Select stocks using the Sharpe Ratio and Beta (CAPM) and then build a portfolio using **Mean–Variance Efficient Frontier**.

- **Portfolio 1 (EF, Sharpe + Beta)**

Combine the **high sharpe + low beta**.

- **Portfolio 2 (EF, Sharpe)**

Select the top N stocks based on the Sharpe and find the point on the efficient frontier.

- **Portfolio 3 (EF, z-score = Sharpe + Beta - Vol)**

Combine the **high sharpe + low beta - volatility** conditions into z-score then optimize on the frontier.

---

### Strategy 2 — Rebalancing Frequency (Portfolios 4–6)
Focus on the impact of **portfolio rebalancing frequency** by maintaining the same stock selection/weighting rules to isolate the influence of rebalancing frequency.

- **Portfolio 4 (Monthly Rebalance)**
- **Portfolio 5 (Quarterly Rebalance)**
- **Portfolio 6 (Annual Rebalance)**

---

## Evaluation Metrics (Annual)

- **CAGR**
- **Volatility**
- **Sharpe Ratio**
- **Max Drawdown (MDD)**
- **Sortino / Calmar**
- **95% VaR + Monte-Carlo**

---

## Results
| Strategy | Portfolio | CAGR | Vol | Sharpe | MDD | Sortino | Calmar | 95% VaR + MonteCarlo |
|---------:|:---------:|:---:|:---:|:-----:|:---:|:-------:|:-------:|:-------:|
| 1        | 1 (EF, Sharpe) | 2.72% | 4.75% | 0.53 | - | - | - | - |
| 1        | 2 (EF, Beta)   | 2.97% | 4.92% | 0.56 | - | - | - | - |
| 1        | 3 (EF, z-score)  | 2.76% | 4.21% | 0.61 | - | - | - | - |
| 2        | 4 (Monthly)      | 24.11% | 22.13% | 0.99 |  -25.53% | 1.34 | 0.94 | -8.33% |
| 2        | 5 (Quarterly)    | 23.24% | 23.37% | 0.90 |  -30.95%	 | 1.28 | 0.75 | -9.15% |
| 2        | 6 (Annually)     | 30.56% | 25.69% | 1.10 |  -26.23%	 | 1.70	| 1.17 | -9.92% |

---

## Conclusion

1. **Working Framework**
   - End-to-end pipeline: data → signals (Sharpe, Beta) → EF construction / rebalancing policy → OOS backtest → evaluation (CAGR, Vol, Sharpe, MDD, etc).

2. **Strategy 1 – Signal-Driven Effiecient Frontier**
   - Select stocks using the Sharpe Ratio, Beta (CAPM), z-score and then build a portfolio using **Mean–Variance Efficient Frontier**.

3. **Strategy 2 – Rebalancing Frequency**
   - Monthly/Quarterly/Annual rebalancing by maintaining the same stock selection/weighting rules to isolate the influence of rebalancing frequency.

4. **Evaluation Metrics (Annual)**
  - **CAGR**
  - **Volatility**
  - **Sharpe Ratio**
  - **Max Drawdown (MDD)**
  - **Sortino / Calmar**
  - **95% VaR + Monte-Carlo**

---

## Executive Summary

We compare **two portfolio construction strategies** across **six portfolios** on S&P 500 stocks

**Strategy 1 (Portfolios 1–3): Signal-Driven Efficient Frontier**
  - Select stocks using **Sharpe Ratio**, **CAPM Beta** and **z-score**, then construct portfolios on the **Mean–Variance Efficient Frontier**.

**Strategy 2 (Portfolios 4–6): Rebalancing Frequency**
  - Hold a consistent baseline selection/weighting rule and vary only the **rebalancing frequency** to isolate implementation effects.
  - **P4 – Monthly**, **P5 – Quarterly**, **P6 – Annually** rebalancing.

**Result** show that **EF portfolios** tend to lower volatility, drawdowns and also low return, while the **rebalancing frequency** more volatility and more risk too.




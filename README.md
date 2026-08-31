## VN Banking Stocks Analysis

Quantitative analysis of return, risk, and correlation for three listed Vietnamese banks — VCB, TCB, and BID — using daily price data from 2022 to 2026.

### Objective

Bank stocks are often assumed to move together given their shared exposure to interest rate and monetary policy cycles. This project tests that assumption quantitatively: how do VCB, TCB, and BID compare in terms of return, volatility, and risk-adjusted performance, and how closely correlated are their price movements?

### Data

Historical daily OHLC price data for VCB, TCB, BID (2022–2026), sourced from Simplize. Prices were cleaned, converted to proper datetime format, and pivoted into a single time-indexed table for analysis.
![Bank stock closing prices, 2022-2026](bieudo_gia_ngan_hang.png)

### Methodology
- Log returns — computed daily log returns for each stock (ln(P_t / P_t-1)), the standard approach in quantitative finance for return aggregation and volatility estimation.
- Return distribution — plotted the distribution of daily log returns for each stock to inspect shape, spread, and tail behavior.
  ![Return distribution](phan_phoi_return.png)
- Volatility — calculated daily and annualized volatility (standard deviation of log returns, annualized with √252).
- Risk-adjusted return — calculated annualized return and Sharpe ratio for each stock (risk-free rate assumed at 5% annually).
- Correlation — computed the pairwise correlation matrix of daily log returns across the three stocks.
- Anomaly detection — flagged trading sessions in 2026 where absolute daily return exceeded 2 standard deviations, to identify unusually volatile sessions.

### Key Findings

**Risk and return (annualized, 2022–2026):**

| Stock |	Annualized Return |	Annualized Volatility |	Sharpe Ratio |
|---|---|---|---|
| VCB |	6.90% |	24.22% | 0.078|
| TCB |	15.18% |	32.13%	| 0.317 |
| BID |	8.44% |	30.25% |	0.114 |

TCB delivered the highest return but also carried the highest volatility; despite that, it posted the best risk-adjusted performance (Sharpe ratio) of the three. VCB was the most stable (lowest volatility) but also the lowest-returning, consistent with its position as the largest and most conservatively priced of the three banks.

**Correlation of daily returns:**

| | VCB | TCB | BID |
|---|---|---|---|
| VCB | 1.00 | 0.40 | 0.60 |
| TCB | 0.40 | 1.00 | 0.52 |
| BID | 0.60 | 0.52 | 1.00 |

![Correlation heatmap](ma_tran_tuong_quan.png)

All three pairs are positively correlated, confirming that Vietnamese bank stocks tend to move together — likely reflecting shared sensitivity to sector-wide factors such as interest rate policy and credit growth. VCB and BID show the strongest co-movement (0.60), while VCB and TCB are the most loosely linked (0.40), suggesting TCB's price behavior is somewhat more idiosyncratic than the other two.

**Volatility clustering**: anomaly detection flagged multiple sessions of unusually large price moves (>2 standard deviations) across all three stocks in early-to-mid 2026, consistent with the sharp price spike visible in the raw price chart during that period — worth investigating further against macro or sector-specific news from that window.

### Tools
Python (pandas, numpy, matplotlib, seaborn) on Google Colab.

### Challenges
Initially, I planned to fetch stock data automatically using the vnstock Python library. However, I ran into two issues: the VCI data source blocks requests from Google Cloud IP addresses (where Colab runs), and other sources in the library returned inconsistent or unsupported errors. After several failed attempts with different data sources, I switched to manually exporting historical price data from a financial data website and uploading it as a file, which proved to be more reliable for this project's scope. This taught me that in real-world data work, the "clean" automated solution isn't always available, and adaptability to a working alternative matters more than sticking to the original plan.

### Future Work
- Time series modeling of volatility (ARIMA/GARCH) to forecast near-term risk
- Extend comparison to a broader set of listed Vietnamese banks and benchmark against VN-Index
- Investigate the macro/news drivers behind the early-2026 volatility spike identified in the anomaly detection step

### How to Run
Open `vn_banking_stocks_analysis.ipynb` in Google Colab or Jupyter. 
Required libraries: `pandas`, `numpy`, `matplotlib`, `seaborn`, `openpyxl`.

**Raw price data files**
Place the raw data files inside a `data/` folder in the same directory as the notebook:

```
data/VCB_history.csv.xlsx
data/TCB_history.csv.xlsx
data/BID_history.csv.xlsx
```
The notebook reads them using the `data/` path, e.g.:

```python
pd.read_excel('data/VCB_history.csv.xlsx', header=5)
```

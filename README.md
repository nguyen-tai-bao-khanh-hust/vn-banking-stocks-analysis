# vn-banking-stocks-analysis
Analysis of stock price trends for 3 listed Vietnamese banks (VCB, TCB, BID), 2022-2026, using Python.

## Data
Historical daily closing prices for VCB, TCB, BID (2022-2026), sourced from Simplize.

![Bank stock price chart](bieudo_gia_ngan_hang.png)

## Key observation
All three stocks show a clear upward trend from 2022 to 2026, with VCB consistently trading at the highest price level. Notably, all three experienced a sharp price spike in early 2026.

## Tools
Python (pandas, matplotlib) on Google Colab

## Challenges
Initially, I planned to fetch stock data automatically using the vnstock Python library. However, I ran into two issues: the VCI data source blocks requests from Google Cloud IP addresses (where Colab runs), and other sources in the library returned inconsistent or unsupported errors. After several failed attempts with different data sources, I switched to manually exporting historical price data from a financial data website and uploading it as a file, which proved to be more reliable for this project's scope. This taught me that in real-world data work, the "clean" automated solution isn't always available, and adaptability to a working alternative matters more than sticking to the original plan.

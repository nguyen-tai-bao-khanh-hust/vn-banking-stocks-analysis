# Raw data (not included)

The raw price files are not redistributed in this repository, in line with Simplize's terms of use.

To reproduce the analysis, export the daily price history for each ticker from Simplize
(https://simplize.vn) and save the Excel files here with these exact names:

    data/VCB_history.csv.xlsx
    data/TCB_history.csv.xlsx
    data/BID_history.csv.xlsx

The notebook reads them with `pd.read_excel(..., header=5)`, so keep the original export format.
Date range used: 25 Aug 2022 – 28 Aug 2026.

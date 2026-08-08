# Global Health Supply Chain Analytics

Power BI dashboard analyzing a real 10,324-row shipment dataset from the USAID Supply Chain Management System (SCMS) — a global health commodity distribution program (primarily HIV/AIDS treatment and diagnostic supplies) spanning 2006-2015 across dozens of countries.

Raw data was sourced from Kaggle, cleaned entirely in Excel (documented step-by-step in the accompanying cleaning log), and visualized in Power BI across three linked report pages.

## Dashboard structure

**Page 1 — Executive Summary**
Six headline KPIs (On-Time Delivery %, Total Shipment Value, Total Shipments, Total Freight Cost, Avg Freight Cost per KG, Avg Delivery Delay) plus two trend charts tracking shipment value and on-time delivery performance year over year. Interactive slicers (Country, Delivery Year, Product Group) filter across all three pages.

**Page 2 — Breakdown Analysis**
Top 10 countries by shipment value, on-time delivery performance by shipment mode, and shipment value distribution by product group.

**Page 3 — Delivery Performance**
A dual-line chart comparing Average vs. Median delivery delay by year, plus a sortable country performance table ranking the worst on-time performers.

## Key findings

- **Overall on-time delivery rate: 88.51%**, with median delivery delay at exactly 0 days in every year of the dataset — the typical shipment arrives on schedule, consistently.
- **Average delivery delay is misleading on its own.** It swings from -15.4 to +0.3 days year to year, driven by a small number of extreme outliers (some shipments logged as 300+ days early, almost certainly data-entry errors rather than real delivery events). The dashboard deliberately shows median alongside average to surface this, rather than reporting a single potentially misleading number.
- **Burundi is the clearest outlier among countries with meaningful shipment volume** — 61.22% on-time (98 shipments), notably below every other country with a comparable sample size.
- **Nigeria leads all countries by total shipment value** ($365M), followed by Zambia and Mozambique.
- **ARV (antiretroviral) shipments dominate the dataset** (86.31% of total shipment value), consistent with the program's HIV/AIDS treatment focus.

## Data cleaning (Excel)

Full step-by-step log in `Cleaning_Log.xlsx`. Highlights:
- Fixed a byte-order-mark encoding artifact on the ID column header
- Dropped two columns that were >99.9% empty
- Split `Weight (Kilograms)` and `Freight Cost (USD)` into numeric columns plus separate notes columns, since both contained business-explanation text (e.g. "Freight Included in Commodity Cost") mixed in with real numbers
- Same split applied to two date columns containing status text like "Pre-PQ Process" and "Date Not Captured"
- Documented, non-random missing-value handling — e.g. missing `Dosage` values were confirmed to concentrate almost entirely in diagnostic test kits, which structurally don't have a dosage
- Found and fixed a double-encoding corruption affecting two text columns (Country, Manufacturing Site) that was present in the original source file
- Ran a full exhaustive data quality scan (encoding, duplicates, negative values, date ranges, categorical consistency) as a final verification step, which is what caught the second encoding issue

## Tech stack

Excel (data cleaning) · Power BI (DAX measures, visualization)

## Files in this repo

- `Supply_Chain_Dashboard.pbix` — the working Power BI file
- `Supply_Chain_Cleaned.xlsx` — the cleaned dataset, ready for analysis
- `Cleaning_Log.xlsx` — full step-by-step record of every cleaning decision and why
- `images/` — screenshots of all three dashboard pages

## Data source

[Supply Chain Shipment Pricing Data](https://www.kaggle.com/datasets/sawandikirby/supply-chain-shipment-pricing-data) — USAID SCMS global health commodity shipment data, via Kaggle.

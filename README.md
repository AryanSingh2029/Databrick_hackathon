# Mutual Fund Analysis on Databricks

This project analyzes mutual fund portfolio disclosures using Databricks.

## Overview

We uploaded 134 mutual fund CSV files into Databricks and built a pipeline to:

- parse semi-structured mutual fund reports
- normalize them into row-level records
- store them as Delta tables
- generate fund-level insights
- perform cross-fund Pareto analysis

## Data Source

The raw data consists of 134 CSV files containing:

- Equity Holdings
- Cash & Cash Equivalents
- Miscellaneous Holdings
- month-wise AUM
- % of AUM
- number of shares

These files are stored in a Databricks Unity Catalog Volume.

## Pipeline

1. Upload raw CSV files to Databricks Volume  
2. Parse report-style CSVs using a custom ingestion notebook  
3. Normalize data into structured rows  
4. Save results as Delta tables:
   - `workspace.default.funds`
   - `workspace.default.holdings`
5. Build dashboards for:
   - Mutual Fund Explorer
   - Pareto Analysis

## Key Features

### Mutual Fund Explorer
- select a mutual fund
- select a month
- view holdings by section
- inspect AUM, % of AUM, and shares

### Pareto Analysis
- aggregate stock exposure across multiple mutual funds
- calculate invested value using:

`invested_cr = (pct_aum / 100) * aum_cr`

- rank stocks by total invested amount
- compute cumulative contribution
- identify stocks needed to reach 80% of total exposure

## Tech Stack

- Databricks
- Unity Catalog Volumes
- Delta Tables
- PySpark
- SQL
- Databricks AI/BI Dashboards

## Tables

### `workspace.default.funds`
Stores one row per mutual fund.

### `workspace.default.holdings`
Stores normalized holdings data with columns like:

- `fund_id`
- `fund_name`
- `section`
- `instrument`
- `month`
- `aum_cr`
- `pct_aum`
- `shares`

## Outcome

The project transforms raw mutual fund portfolio reports into a structured analytics system that supports both:

- individual fund exploration
- combined portfolio concentration analysis

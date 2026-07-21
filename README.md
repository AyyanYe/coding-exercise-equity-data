# Equity Data Analysis - Working Student Exercise

## Overview
This repository contains my Python solution for the Equity Data Analysis coding exercise. The objective was to analyze daily OHLCV dummy data for 100 stocks over the year 2021, identify the top 5 performing titles between `2021-06-01` and `2021-10-13`, and calculate their 30-day average trading volume on the end date.

## Files Included
* **`CodingExerciseAyyan.ipynb`**: The Jupyter Notebook containing the Python code, data cleaning steps, calculations, and visualization logic.
* **`top_5_equity_report.pdf`**: The final generated PDF report containing the summary table and relative performance chart.

## Approach & Assumptions
* **Handling Missing Dates:** I noticed gaps in the data (e.g., Adobe missing data on the exact end date, and Netflix missing a block of days in early July). I structured my code using `groupby().first()` and `.last()`. This gracefully falls back to the nearest valid trading day, rather than hardcoding exact date lookups which would have dropped top performers from the results.
* **Volume Calculation:** I interpreted the "30-day average trading volume" as 30 *trading* days, not calendar days. My script explicitly drops `NaN` values before taking the `.tail(30)` so that data gaps do not artificially skew the average downwards.
* **Plotting Decision:** Instead of plotting absolute prices (which makes vastly different stock prices unreadable on the same axis), I indexed the starting price of all 5 stocks to `100`. This allows the chart to accurately visualize relative percentage growth.

## Data Observations
* **General Electric (GENE):** GENE showed a massive 940% performance increase, largely driven by a massive, instantaneous price spike in early August accompanied by a sharp drop in trading volume. This strongly indicates a reverse stock split. In a production environment, performance would need to be calculated using an `adjusted_close` column to account for corporate actions, otherwise these splits artificially inflate returns.

# Store Footfall vs Sales Conversion

An end-to-end data pipeline on retail footfall and billing data for 12 stores over 90 days. It finds which hours of the day convert visitors into bills the worst.

## Tech Stack
- Databricks (PySpark, Unity Catalog volumes)
- Snowflake (stage, COPY INTO, SQL analysis)

## Pipeline
| Layer | What it does | Result |
|---|---|---|
| Bronze | Raw CSV ingest for footfall, stores and bills | 12,960 footfall rows, 12 stores, 86,859 bills |
| Silver | Removes duplicate bills, orphan store IDs and out-of-hours bills; handles offline and error sensor readings | 265 bill rows removed (86,594 kept) |
| Gold | Store-hour table with bills, revenue and conversion rate | 12,960 rows, 540 with sensor offline |
| Snowflake | Gold table exported as CSV and loaded with COPY INTO | 12,960 rows loaded; reloading processes 0 files (no duplicates) |

## Key Finding
Conversion rate is lowest between 14:00 and 16:00:

| Hour | Conversion rate |
|---|---|
| 15 | 0.0843 |
| 16 | 0.0847 |
| 14 | 0.0863 |

## Files
- `Project.ipynb`: Databricks notebook (Bronze, Silver and Gold layers)
- `capstone.sql`: Snowflake load and analysis queries
- `index.html`: results dashboard (hosted with GitHub Pages)
- `Capstone project screenshots.pdf`: proof of row counts, the repeat-safe load and the final query

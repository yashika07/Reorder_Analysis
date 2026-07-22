# Regional Order & Reorder Pattern Analysis
## Overview

This project analyzes customer reorder behavior across regions using a real-world e-commerce transaction dataset. It simulates a common business analytics scenario: consolidating fragmented regional data into a single source of truth, then using SQL and BI tools to surface actionable patterns for business decision-making.

## About the dataset

The Online Retail II dataset (UCI Machine Learning Repository, via Kaggle) contains ~1 million real transaction line items from a UK-based, non-store online retailer selling all-occasion giftware, covering December 2009 to December 2011. Each row represents one product within an order, and includes the invoice number, product details, quantity, price, order date, customer ID, and the customer's country. The dataset is heavily UK-weighted (~92% of orders), with the remainder spread across EU countries and the rest of the world — a realistic imbalance that this project works with rather than around.

Link to Dataset : https://www.kaggle.com/datasets/mashlyn/online-retail-ii-uci

## Why this project

Businesses with customers spread across regions often struggle to get a unified, reliable view of behavior — data may sit in separate regional systems, contain duplicates or gaps, and need cleaning before it's trustworthy enough to analyze. This project works through that full cycle end-to-end: starting from raw, imperfect data, through cleaning and consolidation, to a concrete business question — do customers in different regions reorder at different rates? — answered with statistical rigor and communicated through a dashboard a non-technical stakeholder could act on.

## What it does
* ETL Pipeline (Python/Pandas): Splits the raw dataset into simulated regional sources (UK / EU / Rest-of-World) to mimic fragmented regional systems, then reads, cleans, and unifies them back into a single dataset — handling missing customer IDs, cancelled orders, and duplicate records along the way.
* SQL Analysis (SQLite): Uses window functions (LAG() with PARTITION BY) to calculate the time gap between each customer's consecutive orders, then aggregates this by region to compare reorder behavior.
* BI Dashboard (Power BI): Visualizes the findings through KPI summary cards, a regional comparison bar chart, a detailed data table, and time-series trend lines (including a zoomed-in view for smaller regions whose patterns were otherwise masked by UK's dominant order volume).

## Key finding

Customers in the "Others" region (outside UK/EU) reordered roughly 34% faster than UK or EU customers (~34.7 days vs. ~52.4 / ~50.4 days average gap between orders). UK and EU customers showed very similar reorder cycles to each other.

### Caveat: 
the "Others" and "EU" segments have notably smaller sample sizes (1,067 and 1,833 reorder events respectively) than UK (28,194), since the source dataset is predominantly UK-based. This finding is directionally useful but would benefit from a larger, more balanced dataset to confirm with full confidence.

## Tools used

Python (Pandas), SQL (SQLite, window functions), Power BI

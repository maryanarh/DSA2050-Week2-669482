# DSA 2050 – Week 2 SQL Lab

**Name:** MarK Mayana 
**Student ID:** 669482

## Objective

This practical lab focused on data acquisition and SQL, with particular attention to relational keys, aggregation grain, `SELECT`, `WHERE`, `GROUP BY`, `JOIN`, missing or duplicate keys, and reconciliation after integration. The goal was to combine customer, order, and region data carefully, investigate deliberate data-quality issues, and produce trustworthy business KPIs. The lab also emphasised that a SQL query can run successfully and still produce the wrong analytical result if keys, row counts, and totals are not validated after joins.

## Key Findings

1. **Duplicate customer key inflated join results.**  
   Customer `C004` appeared twice in `customers.csv`. When joined to orders, this caused order `O005` to match two customer rows, increasing the joined row count from 15 to 16 and inflating total sales from **113,500** to **122,600**. This demonstrated how a non-unique key on the right side of a `LEFT JOIN` can silently multiply rows.

2. **Unmatched customer record was preserved but needs investigation.**  
   Order `O015` had a `CustomerID` of `C999`, which did not exist in the customer table. The `LEFT JOIN` kept this order but produced `NULL` values for `CustomerName` and `Segment`. Rather than deleting it, the record should be investigated as it may represent a missing customer load, a data entry error, or a valid guest order.

3. **Cleaned data revealed segment and regional performance.**  
   After removing the duplicate customer key, the corrected `LEFT JOIN` preserved both the row count (15) and total sales (113,500). Segment KPIs showed that **Corporate** generated the highest total sales (**46,800**) and highest average order value (**11,700**). At the regional level, **Nairobi** generated the highest sales (**39,800**), but revenue alone does not measure profitability, cost to serve, or long-term customer value.

## Repository Contents

- `DSA2050_Week2_SQL_Lab.ipynb` – Completed Jupyter notebook with all code, outputs, and answers.
- `customers.csv` – Source customer data (contains deliberate duplicate).
- `orders.csv` – Source order data (contains an unmatched customer ID).
- `regions.json` – Region lookup table.
- `README.md` – This file.

## How to Run

1. Ensure you have Python 3 and the required libraries installed (`pandas`, `sqlite3`, `json`).
2. Open the notebook `DSA2050_Week2_SQL_Lab.ipynb`.
3. Restart the kernel and run all cells from top to bottom.
4. The notebook will recreate the source files and the SQLite database as needed.

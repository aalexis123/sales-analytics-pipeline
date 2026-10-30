# sales-analytics-pipeline

Sales Analytics Pipeline

A Python/Pandas ETL project that transforms a raw Pakistan e-commerce transactions dataset into four analysis-ready CSV tables: sales, products, customers, and date_dim.
Business problem
Raw transaction exports often contain inconsistent column names, missing values, redundant fields, mixed data types, and orders with different statuses. This project demonstrates a repeatable notebook workflow to prepare transactional data for downstream sales and customer analysis.
Tools
- Python 3
- Pandas
- Jupyter Notebook / Google Colab
What the notebook does
1. Loads the e-commerce CSV and explores its structure, summary statistics, and duplicate rows.
2. Standardizes column names, removes selected redundant fields, and converts date and numeric columns.
3. Removes records missing required transaction fields and filters to configured order statuses.
4. Deduplicates rows using a selected business key and calculates line-item revenue = qty_ordered × price.
5. Builds four output tables and performs basic validation checks before exporting CSV files.
Output tables
File	Contents
sales.csv	Order line items, quantities, prices, revenue, payment method, status
products.csv	Unique SKUs, first observed category, median price
customers.csv	Customer dates, distinct order count, summed line-item revenue
date_dim.csv	Calendar date, year, month, month name, quarter


How to run
1. Open SalesAnalyticsPipeline_GitHub_Ready.ipynb in Google Colab or Jupyter Notebook.
2. Obtain the original Pakistan Largest Ecommerce Dataset CSV from its authorized source. The dataset is not included in this repository.
3. Upload or place the CSV alongside the notebook and set DATA_PATH to its filename (the original filename was Pakistan Largest Ecommerce Dataset1 (1).csv).
4. Install Pandas if needed: pip install pandas.
5. Run all cells in order. The notebook exports four CSV files to the current working directory.
Business rules and limitations
- Revenue definition: qty_ordered × price; excludes adjustments for discounts, shipping, taxes, and refunds.
- Included statuses: complete, received, paid, closed, processing. These are not necessarily all finalized sales.
- Duplicate rule: order_id, sku, qty_ordered. This can discard legitimate repeated line items; validate it against actual transaction identifiers before production use.
- Product dimension: The first category and median observed price are simplified aggregation choices.
- Data source: The notebook currently reads a CSV and exports CSVs. It does not currently connect to PostgreSQL, SQL Server, Power BI, or Power Automate.
- Reproducibility: No specific aggregate revenue or row-count outcome is guaranteed without running the source dataset through the cleaned notebook.
Future improvements
- Load transformed tables into PostgreSQL or Microsoft SQL Server.
- Add automated tests, logging, and configuration files.
- Validate order-status definitions and calculate net revenue using appropriate discount/refund logic.
- Schedule the workflow and connect its output to a Power BI report.
Portfolio context
This project demonstrates data inspection, cleaning, transformation, validation, and the creation of analysis-ready relational-style tables using Python.

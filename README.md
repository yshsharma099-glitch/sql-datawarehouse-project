Full End-to-End BikeStores Data Warehouse Project + EDA & Advanced Analytics

📌 Project Overview

This project demonstrates the end-to-end transformation of raw retail data into a business-ready Star Schema using the Medallion Architecture (Bronze → Silver → Gold).
The goal was to take dirty, unstructured source data and create a high-performance environment for BI reporting, exploratory data analysis, and advanced analytics.


🏗️ Data Architecture
Bronze Layer (Raw)

Purpose: Acts as a landing zone for raw data.
Process: Data is ingested directly from source systems without modifications to preserve the original state for auditing and reprocessing.

Silver Layer (Standardized)

Purpose: Cleans, standardizes, and enriches the data.
Key Transformations:
Data Cleaning: Trimmed whitespaces, normalized emails, standardized state codes.
Data Integrity: Handled type mismatches using TRY_CONVERT and missing values with ISNULL.
Business Logic: Pre-calculated line_total for all orders.
Deduplication: Removed duplicate customer records using ROW_NUMBER().

Gold Layer (Business-Ready)

Purpose: Refined Star Schema optimized for BI tools (Power BI, Tableau).
Design Features:
Flattened Dimensions: Combined Products, Brands, Categories into a single dim_products view to reduce joins.
Performance Tuning: Joined fact tables to dimensions using natural keys.
Star Schema: 2 fact tables + 4 dimensions for reporting and analytics.

📂 Data Model (Star Schema)

Fact Tables:
fact_sales: Order metrics, quantities, and sales_amount.
fact_stocks: Snapshot of current inventory across store locations.

Dimension Tables:
dim_customers: Standardized customer profiles with geographic data.
dim_products: Mega-dimension containing product, brand, and category information.
dim_stores: Retail location details.
dim_staffs: Employee info including hierarchy (Manager IDs) and active status.


Schema Setup: Execute DDL scripts to create Bronze, Silver, and Gold schemas.
Data Ingestion: Load raw data into Bronze tables.
Silver Load: Run silver.load_silver stored procedure to clean and standardize data.
Gold Layer: Run Gold DDL scripts to generate reporting-ready views.

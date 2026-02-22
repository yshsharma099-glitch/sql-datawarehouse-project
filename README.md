🚴‍♂️ BikeStores Data Warehouse Project

📌 Project Overview
This project demonstrates the end-to-end transformation of raw retail data into a business-ready Star Schema using the Medallion Architecture (Bronze → Silver → Gold). The goal was to take "dirty" source data and create a high-performance environment for BI reporting and advanced analytics.

🏗️ Data Architecture

1. Bronze Layer (Raw)
Purpose: Acts as a landing zone for raw data.

Process: Data is ingested directly from the source with no modifications to preserve the original state for auditing and reprocessing.

3. Silver Layer (Standardized)
Purpose: Cleans, standardizes, and enriches the data.

Key Transformations:

Data Cleaning: Handled whitespace with TRIM, normalized email casing with LOWER, and standardized state codes with UPPER.
Data Integrity: Used TRY_CONVERT to handle data type mismatches and ISNULL to manage missing values.
Business Logic: Pre-calculated line_total for all order items to ensure "One Version of the Truth."
Deduplication: Utilized ROW_NUMBER() to identify and remove duplicate customer records.

3. Gold Layer (Business-Ready)
Purpose: A refined Star Schema optimized for BI tools (Power BI, Tableau).

Design Features:

Flattened Dimensions: Combined Products, Brands, and Categories into a single dim_products view to reduce join complexity for analysts.
Performance Tuning: Joined fact tables to dimensions using Natural Keys for maximum query speed.
Star Schema: Organized into 2 Fact tables and 4 primary Dimensions.

📂 Data Model (Star Schema)
Fact Tables

fact_sales: Contains order metrics, quantities, and the pre-calculated sales_amount.
fact_stocks: Provides a snapshot of current inventory levels across all store locations.

Dimension Tables
dim_customers: Standardized customer profiles including full names and geographic data.
dim_products: A "Mega-Dimension" containing product details, brand names, and category names.
dim_stores: Details of retail locations.
dim_staffs: Employee information, including organizational hierarchy (Manager IDs) and active status.

🚀 How to Run
Schema Setup: Run the DDL scripts to create the bronze, silver, and gold schemas.
Data Ingestion: Load the raw data into the bronze tables.
Silver Load: Execute the silver.load_silver stored procedure to clean and move data.
Gold Layer: Run the Gold DDL script to generate the reporting views.

🛠️ Tech Stack
Database: SQL Server (T-SQL)
Architecture: Medallion (Bronze/Silver/Gold)
Modeling: Dimensional Modeling (Star Schema)

📈 Business Insights Enabled
With this warehouse, the following business questions can be answered instantly:

"Which Brand generated the most revenue in New York last quarter?"
"Are our top-selling products currently at risk of stock-outs?"
"What is the total sales performance of each staff member compared to their manager?"

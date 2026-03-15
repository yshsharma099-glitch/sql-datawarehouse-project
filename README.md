# 🚴 Full End-to-End BikeStores Data Warehouse Project + EDA & Tableau Dashboard

## 📌 Project Overview

This project demonstrates the **end-to-end transformation of raw retail data** into a **business-ready Star Schema** using the **Medallion Architecture** (Bronze → Silver → Gold).  
The goal was to take **dirty, unstructured source data** and create a **high-performance environment** for BI reporting, exploratory data analysis, and advanced analytics.

---

## 🏗️ Data Architecture

### **Bronze Layer (Raw)**

- **Purpose:** Landing zone for raw data  
- **Process:** Data ingested directly from source systems to preserve the original state for auditing and reprocessing  

### **Silver Layer (Standardized)**

- **Purpose:** Cleans, standardizes, and enriches data  
- **Key Transformations:**  
  - Trimmed whitespaces, normalized emails, standardized state codes  
  - Handled type mismatches using `TRY_CONVERT` and missing values with `ISNULL`  
  - Pre-calculated `line_total` for all orders  
  - Deduplicated customer records using `ROW_NUMBER()`  
- **Performance:** Indexes created on join keys (`order_id`, `product_id`, `customer_id`, `store_id`, `staff_id`) to optimize star schema joins  

### **Gold Layer (Business-Ready)**

- **Purpose:** Refined **Star Schema** optimized for **BI tools** (Power BI, Tableau)  
- **Design Features:**  
  - Flattened dimensions (`dim_products` combining products, brands, categories)  
  - Star schema: 1 fact table (`fact_sales`) + 5 dimensions  
  - Business metrics: Net sales, gross sales, shipping performance  
  - Surrogate keys for all dimensions for consistency  

**Gold Layer DDL Summary (SQL Views):**

```sql
-- Dimensions
gold.dim_customers
gold.dim_products
gold.dim_stores
gold.dim_staff
gold.dim_date

-- Fact Table
gold.fact_sales''''

Tableau Dashboard

To complement the Gold layer, a fully interactive Tableau dashboard was developed to provide business insights:

Features:

Revenue & Sales Analysis: Total sales, growth vs. previous periods, top-selling products
Customer Insights: Geographic distribution, segmentation by purchase frequency, loyalty metrics
Product & Inventory Tracking: Category-wise stock levels, low-stock alerts
Staff & Store Performance: Employee and store revenue comparison, trend analysis
Interactive Filters & Drilldowns: Filter by product, store, staff, or time period
Delta & Growth Metrics: Visual indicators showing percentage change vs. previous periods

Tech Stack & Integration:

Tableau Version: Tableau Public
Data Source: Connected directly to the Gold layer star schema in SQL Server
Export & Sharing: .twbx file for offline sharing or Tableau Public for interactive access

Impact:
Transforms the Gold layer into intuitive metrics and KPIs, enabling self-service analytics for managers and completing the ETL → EDA → Analytics → BI Reporting cycle.

🛠️ Tech Stack

Database: SQL Server (T-SQL)
Architecture: Medallion (Bronze → Silver → Gold)
Modeling: Dimensional Modeling (Star Schema)
BI / Visualization: Tableau

✅ Key Highlights

End-to-end ETL pipeline from raw to business-ready data
Star schema with optimized Gold layer for reporting
Business metrics including net sales, gross sales, and shipping performance
Interactive Tableau dashboard for actionable insights
Self-contained SQL scripts for Bronze, Silver, and Gold layers

📂 Repository Structure
/SQL
   ├─ bronze_layer.sql       # Raw data ingestion
   ├─ silver_layer.sql       # Data cleaning, standardization
   ├─ gold_layer.sql         # Business-ready star schema
   ├─ analytics_layer.sql    # KPI calculations, aggregations, advanced metrics
/Tableau
   ├─ BikeStores_Dashboard.twbx  # Interactive dashboard
/README.md

This project demonstrates full-stack data engineering and analytics skills:

ETL pipeline from Bronze → Silver → Gold
Star Schema for business-ready reporting
Exploratory Data Analysis (EDA) and KPI calculations
Interactive Tableau dashboard for self-service analytics
It serves as a complete portfolio-ready project for showcasing data engineering, analytics, and BI capabilities.

# olist-ecommerce-lakehouse-data-quality
End-to-end Databricks Lakehouse project using PySpark, Delta Lake, SQL, and data-quality validation on the Olist e-commerce dataset.

# Olist E-Commerce Lakehouse & Data Quality Platform

A Databricks-based data engineering project that transforms raw Brazilian e-commerce data into validated, analytics-ready Delta Lake datasets and business dashboards.

The project implements a Bronze–Silver–Gold lakehouse architecture with data-quality validation, quarantine handling, Spark transformations, and Databricks SQL dashboards.

---

## Project Overview

This project uses the Olist Brazilian E-Commerce dataset to build an end-to-end analytics platform.

The pipeline takes raw CSV datasets through multiple processing layers:

Raw Olist Data → Bronze → Silver + Quarantine → Gold → Databricks SQL Dashboard

The main objective is to demonstrate practical data engineering concepts including:

- Data ingestion
- Delta Lake storage
- PySpark transformations
- Data validation and quality checks
- Data cleansing
- Duplicate detection
- Quarantine handling
- Business-level aggregations
- SQL analytics
- Dashboard development

---

## Architecture

```text
                    Olist E-Commerce Dataset
                              │
                              ▼
                     ┌─────────────────┐
                     │     BRONZE      │
                     │                 │
                     │ Raw Delta Data  │
                     └────────┬────────┘
                              │
                              ▼
                 ┌─────────────────────────┐
                 │   SILVER + QUARANTINE  │
                 │                         │
                 │ Data Quality Validation │
                 │ Cleansing               │
                 │ Duplicate Handling      │
                 │ Business Rules          │
                 └────────────┬────────────┘
                              │
                              ▼
                     ┌─────────────────┐
                     │      GOLD       │
                     │                 │
                     │ Business-ready  │
                     │ Analytics Data  │
                     └────────┬────────┘
                              │
                              ▼
                     ┌─────────────────┐
                     │ Databricks SQL  │
                     │    Dashboard    │
                     └─────────────────┘

🥉 Bronze Layer

The Bronze layer stores the raw Olist datasets in Delta format.

The raw data is preserved before applying business or data-quality transformations.

Datasets include:

Orders
Order Items
Order Payments
Order Reviews
Customers
Geolocation
Sellers
Products
Category Translation
🥈 Silver Layer

The Silver layer contains validated and cleaned datasets.

Data-quality checks were applied before promoting records to the Silver layer.

Data Quality Checks

The following checks were implemented where applicable:

Null value validation
Duplicate record detection
Duplicate identifier detection
Empty string validation
Numeric range validation
Timestamp validation
Coordinate validation
Composite-key validation
Business-rule validation

Problematic records were handled using a quarantine approach instead of silently deleting them.

Examples of Quarantine Handling
Duplicate review records were identified and additional records were moved to quarantine.
Duplicate geolocation records were separated from the validated dataset.
A product record containing only the product ID with all other attributes missing was quarantined.
Legitimate repeated customer identities were retained instead of being incorrectly treated as duplicates.

This approach helps preserve data lineage and makes data-quality issues traceable.

🥇 Gold Layer

The Gold layer contains analytics-ready datasets created from the validated Silver data.

Gold Dataset	Grain
gold_sales	One row per order
gold_delivery	One row per order
gold_reviews	One row per review
gold_seller_performance	One row per seller
gold_product_performance	One row per product
Gold Transformations

The Gold layer includes:

Order-level sales aggregation
Product and freight value aggregation
Payment aggregation
Delivery-time calculations
Delivery delay classification
Review score categorization
Seller performance metrics
Product performance metrics
Product category analysis

## 📊 Databricks SQL Dashboard

### Olist E-Commerce — Executive Analytics Dashboard

The project includes an interactive Databricks SQL dashboard covering executive KPIs, sales, delivery performance, reviews, seller performance, and product performance.

### Executive Overview

![Executive Overview Dashboard](images/executive-overview.png)

### Seller & Product Performance

![Seller & Product Performance Dashboard](images/seller-product-performance.png)

The dashboard contains two pages.

### Page 1 — Executive Overview


Key performance indicators:

- Total Orders
- Product Sales
- Total Freight
- Delivered Orders
- Average Review Score
- Average Delivery Time

Visualizations:

- Orders by Status
- Monthly Product Sales
- Delivery Performance
- Review Score Distribution

### Page 2 — Seller & Product Performance

Visualizations:

- Top 10 Sellers by Product Sales
- Top 10 Sellers by Orders
- Top 10 Products by Sales
- Top 10 Product Categories by Sales

🧠 Key Data Engineering Concepts

This project demonstrates practical experience with:

Lakehouse Architecture
Bronze / Silver / Gold Architecture
Delta Lake
PySpark DataFrame transformations
Spark aggregations
Window Functions
Data Quality Validation
Duplicate Detection
Data Quarantine
Data Cleansing
Business Rule Validation
Data Aggregation
Analytics Data Modeling
SQL Analytics
Dashboard Development

🔍 Data Quality & Reliability

A key objective of the project was to avoid simply removing problematic records.

Instead, records were evaluated based on their data quality and business context.

Valid records were promoted to the Silver layer, while selected problematic records were moved to a dedicated Quarantine layer.

This provides:

Better data traceability
Preservation of problematic records
Easier investigation of data-quality issues
More reliable downstream analytics


📂 Project Structure
Olist-E-Commerce-Lakehouse-Data-Quality-Platform/
│
├── notebooks/
│   ├── 01_Silver_Data_Quality
│   └── 02_Gold_Analytics
│
├── dashboard/
│   └── Olist E-Commerce — Executive Analytics Dashboard
│
└── README.md

🎯 Outcome

Built an end-to-end Databricks Lakehouse data pipeline that transforms raw Olist e-commerce data into validated and analytics-ready Gold datasets.

The project demonstrates practical implementation of:

Raw Data → Data Quality → Quarantine → Business Transformation → Analytics → Dashboard

while maintaining a clear separation between raw, validated, problematic, and analytics-ready data.

👨‍💻 Author

Data Engineering Portfolio Project

Built using Databricks, PySpark, Delta Lake, Python, and SQL.

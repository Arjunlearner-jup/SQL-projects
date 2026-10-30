# Ecommerce Customer and Product Analytics Dashboard

This project is an end-to-end SQL and Streamlit analytics project built from two source tables: `customer_orders` and `order_line_items`.

It creates a final reporting table called `ecommerce_customer_product_metrics` using SQL Common Table Expressions (CTEs), aggregations, joins, conditional logic, and window functions. MySQL 8 supports CTEs with the `WITH` clause, and Streamlit apps can be deployed directly from a GitHub repository on Streamlit Community Cloud.

## Project Overview

The project combines order-level and line-item-level data into a single analytics layer for dashboarding and business analysis.

### Source tables

- `customer_orders`
- `order_line_items`

### Final table

- `ecommerce_customer_product_metrics`

### Dashboard features

- Sidebar filters for month, geography, segment, category, and brand.
- KPI cards for revenue, orders, active customers, units sold, AOV, and return rate.
- Tabs for Overview, Customers, Products, and Data Export.
- CSV download for filtered results.

## Data pipeline

The SQL transformation follows a layered approach using CTEs, which improves readability and lets complex logic be broken into named steps.

### Main SQL steps

1. `base_orders` standardizes order-level fields, adds month logic, and flags completed orders.
2. `base_items` prepares product-level line item data and calculates item revenue.
3. `joined` combines the two source tables using `order_id`.
4. `customer_first_order` finds the first completed order date for each customer.
5. `customer_monthly` calculates monthly customer metrics.
6. `customer_lifetime` calculates lifetime orders, units, revenue, and customer segment.
7. `product_monthly` calculates monthly product performance.
8. `product_ranked` ranks products by category and month using `ROW_NUMBER()`.
9. `order_kpis` builds monthly KPI totals.
10. `final_table` combines customer, order, and product metrics into a reporting-ready table.

## Tech stack

| Layer | Tool |
|---|---|
| Database | MySQL |
| SQL modeling | CTEs, aggregations, window functions |
| App framework | Streamlit |
| Data handling | Pandas |
| Visualization | Plotly |
| DB connection | SQLAlchemy + PyMySQL |

Streamlit supports sidebars, markdown, tabs, and database-connected app layouts for interactive Python dashboards.

## Project structure

```text
ecommerce-sql-streamlit-dashboard/
├─ app.py
├─ requirements.txt
├─ README.md
├─ .gitignore
├─ sql/
│  ├─ 01_schema.sql
│  ├─ 02_seed_data.sql
│  └─ 03_final_table.sql
└─ images/
   └─ dashboard-preview.png
```

## How to run locally

1. Create the source tables in MySQL.
2. Load sample or project data into `customer_orders` and `order_line_items`.
3. Run the SQL script that creates `ecommerce_customer_product_metrics`.
4. Install dependencies.
5. Start the Streamlit app.

### Install dependencies

```bash
pip install streamlit pandas plotly sqlalchemy pymysql
```

### Run the app

```bash
streamlit run app.py
```

## Business questions this project answers

- How much revenue is generated each month?
- Which customer segments generate the most value?
- Which products and categories perform best?
- What share of revenue comes from each customer?
- How do returns, units sold, and order activity change over time?

## Requirements file

```txt
streamlit
pandas
plotly
sqlalchemy
pymysql
```

customer-month row. That is especially important when joining ranked product tables, because broad joins can multiply rows and distort metrics.[cite:186][cite:191]

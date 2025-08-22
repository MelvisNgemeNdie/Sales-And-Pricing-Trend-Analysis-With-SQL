
## Sales & Pricing Trend Analysis with SQL
### Project Overview
This project explores sales and pricing trends over time using cumulative and moving calculations. 
By leveraging SQL window functions and time-series aggregation, it uncovers long-term growth patterns, price trends, and actionable insights for business strategy.


### Project Overview

This project demonstrates the use of advanced SQL techniques to analyze sales and pricing trends over time. Two key analyses are performed:

##### Running Sales Total (Cumulative Sales Over Time)
- Tracks the growth of sales year by year.
- Uses window functions to compute cumulative totals.

##### Moving Average of Prices
- Smooths out fluctuations in yearly average prices.
- Uses rolling 3-year moving averages to reveal long-term pricing trends.
These analyses highlight skills in SQL aggregation, window functions, and time-based analytics, which are essential for data-driven decision-making in business.

### Skills & Technologies

- **SQL (PostgreSQL)**:  Aggregations, CTEs, and window functions.
- **Data Transformation**: Cleaning and grouping data by year.
- **Analytical Techniques**: Running totals, moving averages, and KPI creation.
- **GitHub**: Version control and portfolio documentation.

(Optional) BI Tools (Tableau, Power BI, Excel) – Visualizing the results.

### Dataset
The project uses a fact table:
public."gold.fact_sales"

Key columns used:
- order_date → date of order.
- sales_amount → revenue generated.
- price → unit price of items sold.
customer_key → customer identifier.
- Source: public.gold.fact_sales table
- Key columns:
- order_date – transaction date
- sales_amount – total sales
- price – price per item

Aggregation: Data is summarized by year for cumulative and moving analysis.


## Sales & Pricing Trend Analysis with SQL
### Project Overview
This project explores sales and pricing trends over time using cumulative and moving calculations. 
### Objective
The goal of the project is to uncovers long-term growth patterns, price trends, and actionable insights for business strategy. By leveraging on SQL window functions and time-series aggregation, two key analyses are performed:
##### Running Sales Total (Cumulative Sales Over Time)
- Tracks the growth of sales year by year.
- Uses window functions to compute cumulative totals.
##### Moving Average of Prices
- Smooths out fluctuations in yearly average prices.
- Uses rolling 3-year moving averages to reveal long-term pricing trends.
These analyses highlight skills in SQL aggregation, window functions, and time-based analytics, which are essential for data-driven decision-making in business.
### Dataset
The project uses a **fact table**:
public."gold.fact_sales".

Key columns used:
- order_date → date of order.
- sales_amount → revenue generated.
- price → unit price of items sold.
-customer_key → customer identifier.
### SQL Queries
#### 1. Running Sales Total Over Time
```sql
WITH yearly_sales AS (
    SELECT 
        DATE_PART('year', order_date) AS order_year,
        SUM(sales_amount) AS total_sales
    FROM public."gold.fact_sales"
    WHERE order_date IS NOT NULL
    GROUP BY DATE_PART('year', order_date)
)

SELECT
    order_year,
    total_sales,
    SUM(total_sales) OVER (ORDER BY order_year) AS running_sales_total
FROM yearly_sales
ORDER BY order_year;
```
#### 2. Moving Average Of Prices (3-Year Window)
```sql
WITH yearly_avg_price AS (
    SELECT 
        DATE_PART('year', order_date) AS order_year,
        ROUND(AVG(price), 2) AS avg_price
    FROM public."gold.fact_sales"
    WHERE order_date IS NOT NULL
    GROUP BY DATE_PART('year', order_date)
)

SELECT
    order_year,
    avg_price,
    ROUND(
        AVG(avg_price) OVER (
            ORDER BY order_year 
            ROWS BETWEEN 2 PRECEDING AND CURRENT ROW
        ), 2
    ) AS moving_avg_price_3yr
FROM yearly_avg_price
ORDER BY order_year;



### Skills & Technologies
- **SQL (PostgreSQL)**:  Aggregations, CTEs, and window functions.
- **Data Transformation**: Cleaning and grouping data by year.
- **Analytical Techniques**: Running totals, moving averages, and KPI creation.
- **GitHub**: Version control and portfolio documentation.
- **BI Tools-Tableau**: Visualizing the results.




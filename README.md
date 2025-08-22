
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
```

### Analysis Results
#### 1.Summary Table For Running Sales Totals & Insights
| order_year | total_sales | running_sales_totals |
|------------|-------------|-----------------------|
| 2010       | 43,419      | 43,419                |
| 2011       | 7,075,088   | 7,118,507             |
| 2012       | 5,842,231   | 12,960,738            |
| 2013       | 16,344,878  | 29,305,616            |
| 2014       | 45,642      | 29,351,258            |
- 2010 had very low sales (~43k), suggesting either a partial year of operations or limited market penetration.
- 2011–2013 show strong year-over-year growth, with sales crossing 16M in 2013 alone.
- By 2013, cumulative sales surpassed 29M, highlighting a rapid expansion phase.
- 2014 shows a sudden drop in yearly sales (~45k), which may indicate data issues, seasonality, or a significant business slowdown.
- Despite the dip in 2014, the cumulative trend remains strongly upward, reflecting sustained growth across the earlier years.

#### 2. Summary Table Of Moving Price Averages & Insights
| Year | Avg Price | Moving Avg Price |
|------|-----------|------------------|
| 2010 | 3101      | 3101             |
| 2011 | 3193      | 3147             |
| 2012 | 1720      | 2671             |
| 2013 | 310       | 2081             |
| 2014 | 23        | 1669             |
- Prices peaked around 2010–2011, with averages above 3,000.
- From 2012 onward, prices dropped sharply (down to 23 by 2014).
- The moving average smooths out volatility, clearly showing a steady downward trend across the years.





### Skills & Technologies
- **SQL (PostgreSQL)**:  Aggregations, CTEs, and window functions.
- **Data Transformation**: Cleaning and grouping data by year.
- **Analytical Techniques**: Running totals, moving averages, and KPI creation.
- **GitHub**: Version control and portfolio documentation.
- **BI Tools-Tableau**: Visualizing the results.




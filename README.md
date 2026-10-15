# Retail Sales Analytics in PostgreSQL

A PostgreSQL project that models a small retail business (customers, products, sales and inventory) and answers 139 numbered business questions in SQL. The queries progress from basic filtering to joins, subqueries, CTEs, window functions, stored procedures, transactions and views.

## What this project demonstrates

- **Relational design:** four related tables with primary and foreign keys in a dedicated schema.
- **Querying:** joins (inner, left, self, anti-join), aggregation, GROUP BY and HAVING, set operations.
- **Advanced analytics:** CTEs, correlated subqueries, and window functions (RANK, DENSE_RANK, NTILE, LAG, LEAD, running totals).
- **Business analysis:** customer segmentation, top-N and top-percentile spenders, category and monthly revenue, stock risk, repeat purchasing.
- **Database programming:** functions, a stored procedure, views, indexes and transactions.
- **Data cleaning:** COALESCE, TRIM, LOWER, type casting and date handling.

## Business questions answered (examples)

- Which customers spend more than the average customer, and more than the average of their own membership tier?
- Which products generate the top 50% of revenue?
- Which customers bought in consecutive months?
- Which products are priced above the average of their own category?
- Which products have never been sold, or are running low on stock?
- Who are the top 10% of customers by spend?

## Data model

    customers (1) ---- (many) sales (many) ---- (1) products (1) ---- (1) inventory

- **customers:** customer_id, first_name, last_name, email, phone_number, registration_date, membership_status (Bronze, Silver, Gold)
- **products:** product_id, product_name, category, price, supplier, stock_quantity
- **sales:** sale_id, customer_id, product_id, quantity_sold, sale_date, total_amount
- **inventory:** product_id, stock_quantity

The sample data is synthetic and deliberately small: 50 customers, 15 products in 3 categories (Electronics, Appliances, Accessories), 15 sales between June 2023 and February 2024, and 15 inventory rows. Because of this, some queries correctly return few rows or none. The aim is to show query technique, not to draw business conclusions.

## What is in the script

All work is in one file, `retail_sales_analysis.sql`, organised by question number:

- **Setup:** schema, tables and sample data.
- **Q1 to Q12:** SELECT, filtering, DISTINCT, aggregates, string concatenation.
- **Q13 to Q50:** joins across two and three tables, self-join, GROUP BY and HAVING, date filtering, top-N.
- **Q51 to Q60:** subqueries, including correlated subqueries and NOT EXISTS.
- **Q61 to Q70:** common table expressions.
- **Q71 to Q80:** window functions.
- **Q81 to Q100:** advanced analytical questions (segmentation, Pareto revenue, consecutive months, tier benchmarks).
- **Q101 to Q115:** CASE WHEN, date functions, COALESCE, NOT IN and anti-joins.
- **Q116 to Q119:** PostgreSQL functions and a stored procedure.
- **Q120 to Q125:** indexes, transactions and views.
- **Q126 to Q131:** UNION, INTERSECT, anti-joins, casting and date formatting.
- **Q132 to Q134:** debugging broken queries.
- **Q135 to Q139:** data cleaning.

## How to run

Requires PostgreSQL 11 or later (stored procedures need version 11+).

1. Create an empty database:

        createdb retail_sales

2. Run the script from top to bottom:

        psql -d retail_sales -f retail_sales_analysis.sql

3. To start again, remove the schema first:

        DROP SCHEMA assignment CASCADE;

You can also open the file in pgAdmin or DBeaver and run it one section at a time.

## Notes

- Stock quantity is stored in both `products` and `inventory`. In a production design this would live in one place only.
- The transaction examples (Q122 and Q123) change data when run.
- Q47 uses the current date, so its result depends on when it is run.

## Author

Naftaly Munene, Health Systems Data Lead, Nairobi, Kenya. I work with SQL, Python and Power BI on health programme data.

- GitHub: github.com/NaftalyMunene
  

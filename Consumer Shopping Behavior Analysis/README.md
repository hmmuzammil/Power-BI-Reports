# Consumer Behavior Analysis

## Project Overview

This project analyzes customer purchase behavior, review ratings, discounts, shipping preferences, subscription status, and age segments using shopping transaction data. It includes:

- `script.ipynb`: a Python notebook that loads and cleans the dataset, prepares derived fields like `age_group` and purchase frequency, and writes data to a PostgreSQL table.
- `sql_quries.sql`: a set of analytical SQL queries designed to answer business questions around revenue, discounts, product performance, subscription behavior, customer segments, and age-based revenue contribution.
- `Consumer_Behavior.pbix`: a Power BI dashboard file used for interactive visual analysis and business reporting.

## Data Sources

The analysis is based on customer shopping behavior data imported from a CSV file in the notebook. The notebook currently references the dataset at:

- `D:\Downloads\customer_shopping_behavior.csv`

If you want to run the notebook locally, update this path to the correct CSV location on your machine.

## Notebook Analysis

`script.ipynb` performs the following steps:

1. Loads data with `pandas`.
2. Inspects dataset structure using `df.info()` and `df.describe()`.
3. Fills missing review ratings by category median.
4. Normalizes column names and renames `purchase_amount_(usd)` to `purchase_amount`.
5. Creates an `age_group` segment using quartiles.
6. Maps purchase frequency text values to numeric `frequency_purchase_days`.
7. Drops unnecessary columns such as `promo_code_used`.
8. Saves the cleaned DataFrame to PostgreSQL using SQLAlchemy.

## SQL Analysis Queries

The `sql_quries.sql` file contains queries that answer the following business questions:

1. Total revenue by gender.
2. Customers who used discounts but spent at or above average purchase amount.
3. Top 5 products by average review rating.
4. Average purchase amounts for Standard vs. Express shipping.
5. Subscriber vs. non-subscriber average spend and total revenue.
6. Top 5 products with the highest discount application rate.
7. Customer segmentation by previous purchase count (New, Returning, Loyal).
8. Top products by sales within each category.
9. Subscription status among repeat buyers (more than 5 previous purchases).
10. Revenue contribution by age group.

> Note: Query #10 currently uses `count(purchase_amount)` for revenue contribution; if you want actual revenue, replace it with `sum(purchase_amount)`.

## Power BI Dashboard

The `Consumer_Behavior.pbix` file contains an interactive Power BI dashboard that visualizes key customer and sales metrics. The dashboard likely includes:

- Overall customer and revenue KPIs
- Gender and subscription comparisons
- Category revenue and sales breakdowns
- Product performance and discount analysis
- Age group and customer segment visualizations
- Shipping and review rating insights

Power BI is ideal for exploring these insights visually, filtering by customer attributes, and presenting findings to stakeholders.

## How to Use

1. Open `Consumer_Behavior.pbix` in Power BI Desktop to view interactive dashboards.
2. Open `script.ipynb` in Jupyter or VS Code to inspect data preparation and run the analysis pipeline.
3. Run `sql_quries.sql` against the loaded `customer` table in PostgreSQL to reproduce the query results.

## Recommendations

- Verify the dataset path in `script.ipynb` and move the CSV into the project folder for easier portability.
- Rename the SQL table from `constomer` to `customer` as shown in `sql_quries.sql`.
- Use `sum(purchase_amount)` for revenue-based queries instead of `count(purchase_amount)` when calculating actual revenue.
- Keep the Power BI dashboard and notebook aligned by using the same cleaned data source.

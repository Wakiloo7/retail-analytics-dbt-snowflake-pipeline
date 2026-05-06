# Retail Analytics Engineering Pipeline with Snowflake and dbt

## Overview

This project demonstrates a modern analytics engineering workflow using **Snowflake**, **dbt**, and **SQL**. The goal of the project is to transform raw retail transaction data into clean, tested, and business-ready analytical tables that can support reporting, dashboards, and decision-making. The project focuses on customer purchasing behavior, sales and revenue analysis, product category performance, order and delivery performance, payment method analysis, and data quality validation.

## Architecture

The pipeline follows a layered analytics engineering approach: **Raw Data → Staging Models → Intermediate Models → Dimensional Models → Business Marts**.

The **Raw Layer** contains source datasets loaded into Snowflake without business transformations. Example raw sources include customers, orders, order items, products, payments, sellers, and geolocation data.

The **Staging Layer** standardizes and prepares source data for downstream transformations. Typical operations include renaming columns, casting data types, removing invalid records, standardizing timestamps, and preparing clean source-level models. Example staging models include `stg_customers`, `stg_orders`, `stg_order_items`, `stg_products`, and `stg_payments`.

The **Intermediate Layer** combines multiple staging models and prepares reusable business logic. For example, `int_order_transactions` joins orders, customers, products, and payments while preserving the correct analytical grain.

The **Mart Layer** contains business-facing fact and dimension tables for analytics and reporting. Example mart models include `fact_orders`, `dim_customers`, `dim_products`, and `dim_dates`.

## Data Model

The final analytical model follows a dimensional modeling approach. The main fact table is `fact_orders`, with a grain of one row per order. Example metrics include total order value, number of items, freight value, payment value, delivery duration, order status, customer key, product category key, and date key.

The dimension tables provide descriptive business context. `dim_customers` contains customer location and customer-level attributes. `dim_products` contains product category and product-level descriptive attributes. `dim_dates` supports time-based analysis by day, month, quarter, and year.

## Tech Stack

This project uses **Snowflake** for cloud data warehousing, **dbt** for SQL-based transformations, **SQL** for modeling and analysis, **Git** for version control, and Power BI-ready analytical outputs for reporting and dashboarding.

## Pipeline Workflow

The workflow starts by loading raw datasets into Snowflake. dbt staging models are then used to clean and standardize source data. Intermediate models join and prepare reusable business logic. Dimensional models are then created using fact and dimension tables. dbt tests are applied to validate data quality, and the final analytical outputs are prepared for reporting and dashboarding.

## Data Quality Checks

The project includes data quality checks such as primary key uniqueness, required field not-null validation, duplicate record detection, invalid order amount checks, missing customer references, missing product references, delivery date consistency checks, and payment value validation. Example dbt tests include `unique`, `not_null`, `relationships`, and `accepted_values`.

## Business Questions

The final data marts are designed to answer questions such as: Which product categories generate the most revenue? Which regions or cities contribute most to sales? What is the average delivery time by region? Which payment methods are most commonly used? What percentage of orders are delayed? Which customers or locations show the highest purchase activity?

## Example Insights

The analytical layer can be used to produce insights such as revenue distribution by city and region, product category contribution to total sales, delivery performance by state or location, customer order frequency, payment method distribution, and high-value or low-value order segmentation.

## Project Structure

The project is organized as follows: `models/staging/` contains staging models such as `stg_customers.sql`, `stg_orders.sql`, `stg_order_items.sql`, `stg_products.sql`, and `stg_payments.sql`. `models/intermediate/` contains reusable transformation logic such as `int_order_transactions.sql`. `models/marts/` contains analytical models such as `fact_orders.sql`, `dim_customers.sql`, `dim_products.sql`, and `dim_dates.sql`. The `sql/` folder contains setup, ingestion, validation, and analysis scripts. The `tests/` folder contains data quality tests. The `docs/` folder contains architecture documentation. The `screenshots/` folder contains visual outputs. The repository also includes `dbt_project.yml`, `packages.yml`, and `README.md`.

## Key Features

This project includes an end-to-end analytics engineering workflow, Snowflake-based raw data storage, dbt staging, intermediate, and mart models, fact and dimension modeling, data quality validation, SQL-based business analysis, reporting-ready datasets for Power BI or other BI tools, and clear documentation with a reproducible project structure.

## Skills Demonstrated

This project demonstrates practical skills in cloud data warehousing, SQL transformation workflows, dbt analytics engineering, dimensional data modeling, data mart design, data quality testing, ETL/ELT pipeline design, business-ready reporting datasets, documentation, and version control.

## Future Improvements

Possible improvements include adding Power BI dashboard screenshots, adding more dbt generic and custom tests, adding dbt documentation site screenshots, adding incremental models for large datasets, adding snapshots for slowly changing dimensions, adding CI/CD checks for dbt model validation, and adding orchestration using Airflow or GitHub Actions.

## Summary

This project shows how raw retail data can be transformed into reliable, tested, and analytics-ready data models using Snowflake and dbt. It demonstrates the full analytics engineering workflow from raw ingestion to cleaned staging models, reusable intermediate logic, dimensional marts, data quality checks, and business analysis.
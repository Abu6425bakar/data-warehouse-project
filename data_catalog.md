# Data Catalog for Gold Layer

## Overview

The **Gold Layer** represents the business-ready data model designed for reporting, analytics, and dashboarding purposes.
It contains curated **dimension tables** and **fact tables** that provide clean, standardized, and analytics-friendly data structures.

---

# 1. gold.dim_customers

## Purpose

Stores customer details enriched with demographic and geographic information.

---

## Columns

| Column Name     | Data Type    | Description                                                                           |
| --------------- | ------------ | ------------------------------------------------------------------------------------- |
| customer_key    | INT          | Surrogate key uniquely identifying each customer record in the dimension table.       |
| customer_id     | INT          | Unique numerical identifier assigned to each customer.                                |
| customer_number | NVARCHAR(50) | Alphanumeric identifier representing the customer, used for tracking and referencing. |
| first_name      | NVARCHAR(50) | Customer's first name.                                                                |
| last_name       | NVARCHAR(50) | Customer's last name or family name.                                                  |
| country         | NVARCHAR(50) | Country of residence of the customer (e.g., Australia, United States).                |
| marital_status  | NVARCHAR(50) | Marital status of the customer (e.g., Married, Single).                               |
| gender          | NVARCHAR(50) | Gender of the customer (e.g., Male, Female, n/a).                                     |
| birthdate       | DATE         | Customer's date of birth in `YYYY-MM-DD` format.                                      |
| create_date     | DATE         | Date when the customer record was created in the source system.                       |

---

# 2. gold.dim_products

## Purpose

Provides detailed information about products, categories, and product-related attributes.

---

## Columns

| Column Name          | Data Type    | Description                                                          |
| -------------------- | ------------ | -------------------------------------------------------------------- |
| product_key          | INT          | Surrogate key uniquely identifying each product record.              |
| product_id           | INT          | Unique identifier assigned to the product.                           |
| product_number       | NVARCHAR(50) | Structured alphanumeric code representing the product.               |
| product_name         | NVARCHAR(50) | Descriptive product name including attributes such as size or color. |
| category_id          | NVARCHAR(50) | Unique identifier of the product category.                           |
| category             | NVARCHAR(50) | High-level product classification (e.g., Bikes, Components).         |
| subcategory          | NVARCHAR(50) | Detailed product classification within a category.                   |
| maintenance_required | NVARCHAR(50) | Indicates whether maintenance is required (`Yes` / `No`).            |
| cost                 | INT          | Base cost or price of the product.                                   |
| product_line         | NVARCHAR(50) | Product line classification (e.g., Road, Mountain, Touring).         |
| start_date           | DATE         | Date when the product became available for sale.                     |
| end_date             | DATE         | Date when the product was discontinued or replaced.                  |

---

# 3. gold.fact_sales

## Purpose

Stores transactional sales data used for reporting, analytics, and business intelligence.

---

## Columns

| Column Name   | Data Type    | Description                                             |
| ------------- | ------------ | ------------------------------------------------------- |
| order_number  | NVARCHAR(50) | Unique identifier for each sales order (e.g., SO54496). |
| product_key   | INT          | Foreign key linking to `gold.dim_products`.             |
| customer_key  | INT          | Foreign key linking to `gold.dim_customers`.            |
| order_date    | DATE         | Date when the order was placed.                         |
| shipping_date | DATE         | Date when the order was shipped.                        |
| due_date      | DATE         | Payment due date for the order.                         |
| sales_amount  | INT          | Total monetary amount of the sales transaction.         |
| quantity      | INT          | Quantity of products sold.                              |
| price         | INT          | Unit price of the product sold.                         |

---

# Data Model Summary

The Gold Layer follows a **Star Schema** design:

* **Dimension Tables**

  * `gold.dim_customers`
  * `gold.dim_products`

* **Fact Table**

  * `gold.fact_sales`

This structure enables:

* Fast analytical querying
* Simplified reporting
* Power BI integration
* Historical trend analysis
* KPI and dashboard generation

---

# Notes

* All tables are optimized for analytical workloads.
* Surrogate keys are used for dimensional modeling best practices.
* Data is transformed and cleansed during Bronze → Silver → Gold ETL processing.
* Null and invalid values are standardized during Silver Layer transformations.

---

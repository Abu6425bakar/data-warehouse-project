# Naming Conventions

This document outlines the naming conventions used for schemas, tables, views, columns, and other database objects in the data warehouse project.

---

# Table of Contents

1. [General Principles](#general-principles)
2. [Table Naming Conventions](#table-naming-conventions)

   * [Bronze Rules](#bronze-rules)
   * [Silver Rules](#silver-rules)
   * [Gold Rules](#gold-rules)
3. [Glossary of Category Patterns](#glossary-of-category-patterns)
4. [Column Naming Conventions](#column-naming-conventions)

   * [Surrogate Keys](#surrogate-keys)
   * [Technical Columns](#technical-columns)
5. [Stored Procedure Naming Conventions](#stored-procedure-naming-conventions)

---

# General Principles

The following principles apply to all database objects across the data warehouse environment.

* Use **snake_case** formatting.
* Use only **lowercase letters**.
* Separate words using underscores (`_`).
* Use **English** language for all naming.
* Avoid abbreviations unless they are widely understood.
* Avoid SQL reserved keywords as object names.
* Use meaningful and descriptive names.
* Maintain consistency across all layers.

---

# Table Naming Conventions

## Bronze Rules

Bronze tables represent raw ingested data from source systems.

### Rules

* Table names must start with the source system name.
* Table names must match the original source table names.
* No renaming or business transformation should occur in the Bronze layer.

### Pattern

```text
<sourcesystem>_<entity>
```

### Components

| Component        | Description                                      |
| ---------------- | ------------------------------------------------ |
| `<sourcesystem>` | Name of the source system such as `crm` or `erp` |
| `<entity>`       | Original table name from the source system       |

### Examples

| Table Name           | Description                          |
| -------------------- | ------------------------------------ |
| `crm_customer_info`  | Customer information from CRM system |
| `erp_product_master` | Product master data from ERP system  |

---

## Silver Rules

Silver tables represent cleansed and standardized data.

### Rules

* Table names must retain the source system prefix.
* Table names should remain aligned with the original source entities.
* Data cleansing and transformation are allowed, but naming consistency must be preserved.

### Pattern

```text
<sourcesystem>_<entity>
```

### Examples

| Table Name          | Description                    |
| ------------------- | ------------------------------ |
| `crm_customer_info` | Cleaned customer data from CRM |
| `erp_sales_orders`  | Standardized ERP sales orders  |

---

## Gold Rules

Gold tables are business-ready analytical models.

### Rules

* Use meaningful business-oriented names.
* Table names must begin with a category prefix.
* Names should align with reporting and analytics terminology.

### Pattern

```text
<category>_<entity>
```

### Components

| Component    | Description                                       |
| ------------ | ------------------------------------------------- |
| `<category>` | Table category such as `dim`, `fact`, or `report` |
| `<entity>`   | Business entity name                              |

### Examples

| Table Name             | Description                   |
| ---------------------- | ----------------------------- |
| `dim_customers`        | Customer dimension table      |
| `dim_products`         | Product dimension table       |
| `fact_sales`           | Sales fact table              |
| `report_monthly_sales` | Monthly sales reporting table |

---

# Glossary of Category Patterns

| Pattern   | Meaning          | Examples                        |
| --------- | ---------------- | ------------------------------- |
| `dim_`    | Dimension tables | `dim_customers`, `dim_products` |
| `fact_`   | Fact tables      | `fact_sales`                    |
| `report_` | Reporting tables | `report_sales_monthly`          |

---

# Column Naming Conventions

## Surrogate Keys

Surrogate keys uniquely identify records in dimension tables.

### Rules

* All surrogate keys must end with the suffix `_key`.
* Keys should use meaningful entity names.

### Pattern

```text
<table_name>_key
```

### Examples

| Column Name    | Description                          |
| -------------- | ------------------------------------ |
| `customer_key` | Surrogate key for customer dimension |
| `product_key`  | Surrogate key for product dimension  |

---

## Technical Columns

Technical columns store metadata and ETL-related information.

### Rules

* All technical columns must begin with the prefix `dwh_`.
* Names should clearly describe the column purpose.

### Pattern

```text
dwh_<column_name>
```

### Examples

| Column Name       | Description                                     |
| ----------------- | ----------------------------------------------- |
| `dwh_load_date`   | Date when the record was loaded                 |
| `dwh_create_date` | Timestamp when the warehouse record was created |
| `dwh_update_date` | Timestamp of latest warehouse update            |

---

# Stored Procedure Naming Conventions

Stored procedures responsible for ETL loading operations must follow a standardized naming structure.

### Pattern

```text
load_<layer>
```

### Components

| Component | Description                                  |
| --------- | -------------------------------------------- |
| `load`    | Indicates ETL loading process                |
| `<layer>` | Target layer such as bronze, silver, or gold |

### Examples

| Procedure Name | Description                  |
| -------------- | ---------------------------- |
| `load_bronze`  | Loads data into Bronze layer |
| `load_silver`  | Loads data into Silver layer |
| `load_gold`    | Loads data into Gold layer   |

---

# Additional Recommendations

* Keep naming concise but descriptive.
* Avoid spaces and special characters.
* Use singular or plural naming consistently across the project.
* Maintain the same naming standards in SQL scripts, Power BI models, and ETL pipelines.
* Document all naming standards for team-wide consistency.

---

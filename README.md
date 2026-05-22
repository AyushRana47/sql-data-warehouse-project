# SQL Data Warehouse Project

> Building a modern data warehouse with SQL Server — covering ETL pipelines, Medallion Architecture, data modeling, and analytics.

---

## Table of Contents

- [Overview](#overview)
- [Architecture](#architecture)
- [Project Structure](#project-structure)
- [Data Sources](#data-sources)
- [ETL Pipeline](#etl-pipeline)
- [Data Modeling](#data-modeling)
- [Analytics & Reporting](#analytics--reporting)
- [Getting Started](#getting-started)
- [License](#license)

---

## Overview

This project demonstrates how to design and build a production-style **data warehouse using SQL Server (T-SQL)**. It consolidates data from two source systems — ERP and CRM — into a single analytical model that supports business reporting and decision-making.

**Key objectives:**

- Ingest raw data from CSV source files into SQL Server
- Cleanse and standardize data to ensure quality
- Integrate ERP and CRM data into a unified, query-optimized model
- Deliver SQL-based analytics for customer and product insights

---

## Architecture

The warehouse follows the **Medallion Architecture**, organized into three progressive layers:

```
Bronze  →  Silver  →  Gold
```

| Layer | Purpose |
|--------|---------|
| **Bronze** | Raw data ingested as-is from source CSV files. No transformations applied. |
| **Silver** | Cleaned, standardized, and normalized data. Resolves duplicates, nulls, and type issues. |
| **Gold** | Business-ready data modeled as a star schema. Optimized for analytical queries and reporting. |

> Architecture diagrams, data flow maps, and ERDs are available in the [`docs/`](./docs) folder.

---

## Project Structure

```
sql-data-warehouse-project/
│
├── datasets/                   # Source CSV files (ERP and CRM raw data)
│
├── docs/                       # Project documentation
│   ├── data_architecture.drawio
│   ├── data_catalog.md
│   ├── data_flow.drawio
│   ├── data_models.drawio
│   ├── etl.drawio
│   └── naming-conventions.md
│
├── scripts/                    # T-SQL scripts for all layers
│   ├── bronze/                 # Load raw data into Bronze layer
│   ├── silver/                 # Clean and transform data into Silver layer
│   └── gold/                   # Build analytical models in Gold layer
│
├── tests/                      # Data quality and integrity test scripts
│
├── LICENSE
└── README.md
```

---

## Data Sources

Two source systems are used, provided as CSV files in the `datasets/` directory:

| Source | Description |
|--------|-------------|
| **ERP System** | Contains transactional data such as orders, products, and customers |
| **CRM System** | Contains customer relationship data including sales interactions and regions |

---

## ETL Pipeline

The ETL process moves data through all three layers of the Medallion Architecture:

1. **Extract** — CSV files are loaded into the Bronze layer using bulk insert scripts
2. **Transform** — Silver layer scripts handle deduplication, null resolution, type casting, and standardization
3. **Load** — Gold layer scripts build fact and dimension tables using the cleaned Silver data

Each stage has dedicated SQL scripts under `scripts/bronze/`, `scripts/silver/`, and `scripts/gold/`.

---

## Data Modeling

The Gold layer is modeled as a **Star Schema**, designed for efficient analytical queries:

- **Fact Tables** — Transactional records (e.g., sales facts)
- **Dimension Tables** — Descriptive context (e.g., customers, products, dates)

Refer to `docs/data_models.drawio` for the full entity-relationship diagram.

---

## Analytics & Reporting

SQL-based reports are included that deliver insights across two key domains:

**Customer Analytics**
- Customer segmentation by region and revenue
- Buying behavior and order frequency

**Product Analytics**
- Top-performing products by sales volume and revenue
- Category-level performance comparisons

---

## Getting Started

### Prerequisites

- SQL Server (2019 or later recommended)
- SQL Server Management Studio (SSMS) or Azure Data Studio

### Steps

1. **Clone the repository**
   ```bash
   git clone https://github.com/AyushRana47/sql-data-warehouse-project.git
   cd sql-data-warehouse-project
   ```

2. **Initialize the database**  
   Run the database initialization script to create the `DataWarehouse` database and schemas (`bronze`, `silver`, `gold`):
   ```sql
   -- Run in SSMS
   scripts/init_database.sql
   ```

3. **Load Bronze layer**  
   Execute the scripts in `scripts/bronze/` to ingest raw CSV data.

4. **Transform to Silver layer**  
   Execute the scripts in `scripts/silver/` to clean and standardize the data.

5. **Build Gold layer**  
   Execute the scripts in `scripts/gold/` to create the analytical star schema.

6. **Run tests**  
   Validate data quality using the scripts in `tests/`.

7. **Explore analytics**  
   Query the Gold layer tables for business insights.

---

## License

This project is licensed under the [MIT License](./LICENSE).


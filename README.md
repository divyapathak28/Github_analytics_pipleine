# GitHub Analytics Data Warehouse

## Overview

This project is a POC for building a GitHub Analytics Data Warehouse using an ELT-based approach.

The data is extracted from the GitHub API using Airbyte and loaded into MySQL. dbt is then used to clean, transform, and organize the data into different layers for analytics and reporting.

## Architecture

```text
GitHub API
    |
    v
 Airbyte
    |
    v
   MySQL
    |
    v
   dbt
    |
    v
Bronze -> Silver -> Gold -> Mart
```

### Components

| Component | Purpose |
|---|---|
| GitHub API | Source of GitHub repository data |
| Airbyte | Extracts and loads the data |
| MySQL | Stores the raw and transformed data |
| dbt | Handles data cleaning and transformations |
| Mart Layer | Provides datasets for reporting and analytics |

## Data Layers

### Bronze

The Bronze layer contains the raw data with minimal changes.

Tables:

- `bronze_repositories`
- `bronze_contributors`
- `bronze_issues`
- `bronze_pull_requests`

### Silver

The Silver layer contains cleaned and standardized versions of the Bronze data.

Tables:

- `silver_repositories`
- `silver_contributors`
- `silver_issues`
- `silver_pull_requests`

### Gold

The Gold layer is used for analytics and contains fact and dimension tables.

**Dimension tables**

- `dim_repository`
- `dim_contributor`
- `dim_date`

**Fact tables**

- `fact_issues`
- `fact_pull_requests`
- `fact_contributor_activity`

### Mart

The Mart layer contains simplified datasets that can be used for reporting and dashboards.

Tables:

- `mart_repo`
- `mart_contributor`

## Transformations

The dbt models perform a few key transformations, including:

- Removing duplicate records
- Standardizing column names
- Converting data types
- Handling null values
- Creating fact and dimension models
- Building reporting-ready marts

## Workflow

The overall workflow is:

1. Extract GitHub data using Airbyte.
2. Load the raw data into MySQL.
3. Transform the data using dbt through the Bronze, Silver, and Gold layers.
4. Create Mart tables for reporting and analytics.

## Benefits

The layered approach makes the warehouse easier to maintain and extend. It also improves data quality and provides reusable dbt models for analytics.

The Mart tables can be used to simplify reporting, and additional GitHub metrics can be added later as the project grows.

## Tech Stack

- GitHub API
- Airbyte
- MySQL
- dbt

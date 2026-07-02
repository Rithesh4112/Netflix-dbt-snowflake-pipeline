# Netflix Data Engineering Pipeline using Snowflake and dbt

## Project Overview

This project is an end-to-end data engineering pipeline built using **Snowflake**, **dbt Core**, and **SQL**. The goal of the project is to transform raw Netflix/MovieLens-style movie datasets into clean, analytics-ready data models that can support reporting, dashboarding, and business analysis.

The project follows a modern analytics engineering workflow where raw data is loaded into Snowflake, transformed using dbt models, tested for data quality, and organized into staging, dimension, fact, mart, seed, and snapshot layers.

## Business Problem

Streaming platforms generate large volumes of data related to movies, user ratings, tags, genres, and relevance scores. Raw datasets are often not ready for direct reporting because they may contain inconsistent naming, duplicate records, unstructured tags, and multiple source tables.

This project solves that problem by creating a structured data pipeline that converts raw movie data into clean and reliable analytical models for insights such as:

* Movie rating behavior
* Movie genre analysis
* User rating patterns
* Tag-based movie classification
* Genome score relevance analysis
* Movie release date enrichment
* Historical tracking of tag changes using snapshots

## Tech Stack

* **Snowflake** — Cloud data warehouse
* **dbt Core** — Data transformation and modeling
* **SQL** — Data cleaning, transformation, joins, and aggregations
* **Git & GitHub** — Version control and project hosting
* **dbt Seeds** — Static reference data loading
* **dbt Snapshots** — Historical change tracking
* **dbt Tests** — Data quality validation

## Project Architecture

```text
Raw MovieLens/Netflix Data
        |
        v
Snowflake RAW Schema
        |
        v
dbt Staging Models
        |
        v
Dimension and Fact Models
        |
        v
Mart Models
        |
        v
Analytics-Ready Tables for Reporting
```

## Data Pipeline Flow

### 1. Raw Data Layer

Raw datasets are stored in Snowflake under the RAW schema. These datasets include movies, ratings, links, tags, genome scores, and genome tags.

### 2. Staging Layer

The staging layer standardizes raw source tables by renaming columns, cleaning data types, and preparing the data for downstream transformation.

Staging models include:

* `src_movies`
* `src_ratings`
* `src_tags`
* `src_links`
* `src_genome_score`
* `src_genome_tags`

### 3. Dimension Models

Dimension models provide descriptive business entities that can be reused across reports and analysis.

Dimension models include:

* `dim_movies`
* `dim_users`
* `dim_genome_tags`
* `dim_movies_with_tags`

### 4. Fact Models

Fact models store measurable business events and metrics.

Fact models include:

* `fct_ratings`
* `fct_genome_scores`

### 5. Mart Model

The mart layer combines transformed data into business-ready tables for reporting and dashboarding.

Mart model:

* `mart_movie_release`

### 6. Seed Data

A dbt seed file is used to load static movie release date reference data into Snowflake.

Seed file:

* `seeds_movie_release_dates.csv`

### 7. Snapshot

A dbt snapshot is used to track historical changes in movie tag data over time.

Snapshot model:

* `snap_tags`

## Key Features

* Built modular dbt models using staging, dimension, fact, and mart layers
* Created reusable SQL transformations for movie, rating, tag, and genome datasets
* Loaded static reference data using dbt seeds
* Implemented dbt snapshots to track historical changes
* Applied dbt tests for data quality validation
* Used Snowflake as the cloud data warehouse for scalable data storage and processing
* Version-controlled the complete project using Git and GitHub

## dbt Commands Used

Install dbt dependencies:

```bash
dbt deps
```

Run all dbt models:

```bash
dbt run
```

Run a specific model:

```bash
dbt run --select model_name
```

Load seed data:

```bash
dbt seed --full-refresh
```

Run dbt tests:

```bash
dbt test
```

Run snapshots:

```bash
dbt snapshot
```

Generate dbt documentation:

```bash
dbt docs generate
dbt docs serve
```

## Project Structure

```text
netflix/
│
├── analyses/
├── macros/
│   └── no_nulls_in_coloumns.sql
│
├── models/
│   ├── staging/
│   │   ├── src_movies.sql
│   │   ├── src_ratings.sql
│   │   ├── src_tags.sql
│   │   ├── src_links.sql
│   │   ├── src_genome_score.sql
│   │   └── src_genome_tags.sql
│   │
│   ├── dim/
│   │   ├── dim_movies.sql
│   │   ├── dim_users.sql
│   │   ├── dim_genome_tags.sql
│   │   └── dim_movies_with_tags.sql
│   │
│   ├── fct/
│   │   ├── fct_ratings.sql
│   │   └── fct_genome_scores.sql
│   │
│   ├── mart_movie_release.sql
│   ├── schema.yml
│   └── sources.yaml
│
├── seeds/
│   └── seeds_movie_release_dates.csv
│
├── snapshots/
│   └── snap_tags.sql
│
├── tests/
│   └── relevance_score_test.sql
│
├── dbt_project.yml
├── packages.yml
├── package-lock.yml
└── README.md
```

## Data Quality Checks

This project includes dbt tests to validate important data quality rules such as:

* Ensuring key columns are not null
* Validating relationships between fact and dimension tables
* Checking rating and relevance score values
* Ensuring transformed models are reliable for downstream analytics

## Business Insights Enabled

This pipeline can support analysis such as:

* Top-rated movies
* Most active users by rating count
* Movie popularity by number of ratings
* Genre-based rating trends
* Movies enriched with release dates
* Tag-based movie categorization
* Relevance score analysis using genome data
* Historical tracking of tag changes

## What I Learned

Through this project, I practiced and implemented:

* Building an end-to-end data engineering pipeline
* Connecting dbt Core with Snowflake
* Creating staging, dimension, fact, and mart models
* Writing modular SQL transformations
* Using dbt seeds for static reference data
* Using dbt snapshots for slowly changing data
* Running dbt tests for data validation
* Managing a data engineering project using Git and GitHub

## Future Improvements

* Add Airflow orchestration to schedule dbt runs
* Build a Power BI or Tableau dashboard on top of the mart tables
* Add more advanced dbt tests and documentation
* Add CI/CD using GitHub Actions
* Add data freshness checks for source tables
* Expand the mart layer for more business KPIs


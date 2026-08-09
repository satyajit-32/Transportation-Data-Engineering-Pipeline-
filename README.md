# Transportation Data Pipeline – End-to-End Data Engineering Project

An end-to-end **Data Engineering pipeline** built for a fictional ride-hailing company, **GoodCabs**, using **Databricks, PySpark, SQL, and Lakeflow Spark Declarative Pipelines (SDP)**. The project follows the **Medallion Architecture (Bronze → Silver → Gold)** to transform raw trip and city data into clean, business-ready, region-wise analytics.

---

##  Problem Statement

GoodCabs operates across multiple cities in India (similar to Uber). Regional managers were not receiving timely, city-specific insights — data was late, dashboards were generic, and teams had to manually rework exports. This project solves that by building a fast, scalable, and automated data pipeline that delivers **region-wise analytics** with minimal manual intervention.

---

##  Architecture

**Source (Amazon S3) → Databricks (Bronze → Silver → Gold) → Unity Catalog → Genie (AI Analytics)**

- **Bronze Layer**: Raw ingestion of `city` (dimension) and `trips` (fact) data from Amazon S3 using Auto Loader (streaming) for incremental file detection.
- **Silver Layer**: Cleaned, validated, and standardized data — includes a `calendar/date` dimension table generated programmatically, column renaming, data quality checks (expectations), and CDC (Change Data Capture) handling via **Auto CDC Flow**.
- **Gold Layer**: Denormalized fact table (`fact_trips`) joining trips, city, and calendar tables, plus **city-specific views** for each regional manager to power their own BI dashboards.

---

##  Tech Stack

- **Databricks Free Edition**
- **Lakeflow Spark Declarative Pipelines (SDP)** — Python & SQL
- **PySpark** — data transformations
- **Amazon S3** — raw data landing zone
- **Unity Catalog** — governance, cataloging, and role-based access control (RBAC)
- **Databricks Genie** — natural language (AI-powered) analytics
- **Auto Loader** — incremental/streaming ingestion
- **Delta Lake** — storage format with Change Data Feed (CDF)

---

##  Key Features

- **Declarative pipeline design** — focuses on *what* to do rather than *how*, drastically reducing boilerplate code (e.g., ~50 lines vs ~135 lines for equivalent imperative CDC logic).
- **Medallion Architecture** (Bronze, Silver, Gold) implemented with Materialized Views and Streaming Tables.
- **Auto CDC Flow** for upsert (SCD Type 1) handling on the fact table, keyed on trip ID.
- **Data quality expectations** (`expect`, `expect_or_drop`, `expect_or_fail`) to validate ratings and business dates.
- **Auto Loader** for incremental ingestion — only new files are processed, avoiding full reprocessing.
- **Dynamically generated calendar/date dimension table** for time-based analytics (weekday/weekend, quarter, holidays, etc.).
- **City-specific gold views** enabling self-serve analytics per regional manager.
- **Role-Based Access Control (RBAC)** via Unity Catalog groups for secure, scalable data governance.
- **AI-powered analytics** using Databricks Genie for natural language querying.
- **Continuous pipeline mode** for near real-time incremental processing as new data lands in S3.

---

##  Data Sources

- `city.csv` — Dimension table with city IDs and names.
- `trips_*.csv` — Daily fact files with trip ID, date, city ID, passenger type, distance, fares, driver/passenger ratings, etc.

---

##  Pipeline Flow

1. **Ingestion**: CSV files uploaded to S3 → connected to Databricks via external location.
2. **Bronze**: Raw ingestion with metadata columns (file name, ingestion timestamp) using Materialized Views (dimension) and Streaming Tables with Auto Loader (fact).
3. **Silver**: Column renaming, data quality validation, timestamp tracking, and CDC-based upserts into cleaned streaming tables.
4. **Gold**: Joins across fact and dimension tables to create a single denormalized `fact_trips` table, plus per-city views for regional reporting.
5. **Governance**: Unity Catalog permissions and RBAC groups control access to gold-layer views per region.
6. **Analytics**: Databricks Genie used for natural-language, AI-driven querying on top of the gold layer.

---

##  Sample Business Questions Answered

- What is the average passenger/driver rating per city?
- What is the total revenue and total number of rides per region?
- Which day of the week has the highest ratings?
- How do ratings and revenue trend by month/quarter?

---

##  Key Learnings

- Difference between **declarative vs. imperative** programming paradigms.
- Core Lakeflow SDP concepts: **Flow, Materialized View, Streaming Table, Sync, Pipeline**.
- Building **Auto CDC pipelines** for near-real-time, incrementally updated fact tables.
- Implementing **data governance and RBAC** using Unity Catalog.
- Leveraging **AI-assisted analytics** (Genie) directly within the data platform.

---

##  Acknowledgment

This project was built as part of a hands-on learning exercise following a guided tutorial on Databricks Lakeflow Spark Declarative Pipelines, using the Databricks Free Edition.

---

##  Contact

Feel free to connect or reach out if you have questions about this project or the implementation!

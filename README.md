# Transportation-Data-Engineering-Pipeline-

An end-to-end data engineering project built using **Databricks Lakeflow Spark Declarative Pipelines**, **PySpark**, **AWS S3**, **Delta Lake**, **SQL**, and **Unity Catalog**.

The project demonstrates how raw transportation data can be ingested from Amazon S3, transformed through a **Bronze-Silver-Gold Medallion Architecture**, and converted into analytics-ready datasets while implementing incremental processing, data governance, and role-based access control.

---

##  Project Overview

This project simulates a transportation/ride-booking data platform where raw data is stored in **Amazon S3** and processed using **Databricks Lakeflow Spark Declarative Pipelines**.

The pipeline follows the Medallion Architecture:

```text
                  AWS S3
                    │
                    ▼
             ┌──────────────┐
             │    BRONZE    │
             │  Raw Data    │
             └──────┬───────┘
                    │
                    ▼
             ┌──────────────┐
             │    SILVER    │
             │ Cleaned &    │
             │ Transformed  │
             └──────┬───────┘
                    │
                    ▼
             ┌──────────────┐
             │     GOLD     │
             │ Fact &       │
             │ Dimensions   │
             └──────┬───────┘
                    │
                    ▼
             Analytics / BI
## Technologies Used
Databricks
Lakeflow Spark Declarative Pipelines
PySpark
SQL
AWS S3
Delta Lake
Unity Catalog
Databricks Genie
Medallion Architecture

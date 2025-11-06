**### Databricks Delta Live Tables Declarative Pipeline**

### Overview
This project implements an end-to-end streaming data pipeline in Databricks Delta Live Tables (DLT) to automate data ingestion, transformation, and curation using the 
Bronze - Silver - Gold Lakehouse architecture.

The pipeline processes raw JSON and CSV files arriving in the landing zone, incrementally transforming them into high-quality Delta tables suitable for analytics and reporting.

### 🗂️ Project Structure
├── 1_DLT_Demo_Project_Setup/
│   └── setup_notebook.py
│
└── 2_DLT_Demo
    └── transformations/
    ├── bronze_pipeline.dlt
    ├── silver_pipeline.dlt
    └── gold_pipeline.dlt

### 1. Setup Folder

Purpose:
Initializes all foundational Unity Catalog and storage configurations required for the data pipeline.

Key actions:
Creates storage credentials for secure access to Azure Data Lake (landing zone and delta lake zones).
Defines external locations and volumes.
Creates catalogs and schemas (e.g., circuitbox).


### 2. Transformative Folder:
Contains all DLT pipeline definitions that handle ingestion, cleansing, and business curation.

### Pipeline Key Features
- bronze_pipeline.dlt -	Ingests raw data from landing zone	Uses Auto Loader (cloud_files()) for incremental and schema-evolving ingestion of JSON and CSV files
- silver_pipeline.dlt	- Cleanses and standardizes bronze data	Implements data quality constraints, and demonstrates SCD Type 1 and SCD Type 2 handling
- gold_pipeline.dlt	- Produces business-ready datasets	Joins curated data and prepares summary tables for analytics and dashboards

### Data Flow
Landing Zone → Deltalake

bronze.sql:
Streaming ingestion from /Volumes/circuitbox/landing/operational_data/.
JSON files for customers and orders; CSV files for addresses.
Raw schema inferred automatically using cloud_files() with schema evolution enabled.

silver.sql:
Customers & Orders: Implement SCD Type 1 — latest record overwrites existing data.
Addresses: Implements SCD Type 2 — tracks historical changes using effective and expiry timestamps.
Data quality enforced through EXPECT constraints (e.g., valid customer_id, address completeness).

gold.sql:
Combines curated tables to create analytics-ready datasets.
Aggregates metrics like order volume, active customers, and address distribution for dashboarding.

### Execution Steps:

1. Run the Setup Notebook to register:
Storage credentials
External locations
Volumes
Catalogs and schemas

2. Run the pipelines under transformation folder:
Deploy and run the Bronze, Silver, and Gold pipelines in sequence using the Databricks Delta Live Tables UI.
Each pipeline is configured for continuous streaming mode, ensuring near real-time data freshness.


### Domain	Format	Change Type	Description:
- Customers	JSON	SCD Type 1	Overwrites old records on update
- Orders	JSON	SCD Type 1	Maintains latest transactional data
- Addresses	CSV	SCD Type 2	Preserves history with effective and expiry timestamps

### Key Highlights:
Streaming ingestion with Auto Loader for continuous processing.
Declarative transformations using DLT syntax (CREATE OR REFRESH STREAMING TABLE).
Data quality enforcement through EXPECT constraints and validation rules.
SCD Type 1 and Type 2 modeling in the Silver layer for real-world scenarios.
Business-ready Gold tables for visualization and analytics in Power BI or Sigma.
End-to-end lineage and monitoring via Databricks DLT UI.
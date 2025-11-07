# Databricks_Demo

A demonstration repository showcasing Databricks projects using Spark and structured streaming pipelines, including declarative pipelines and Autoloader-based ingestion. This repo contains three projects that illustrate best practices for building production-ready pipelines in Databricks.

Projects
1. Declarative Pipelines

Description:
Implements a declarative approach for building Spark ETL pipelines.

Pipelines are modular and configurable.

Includes parameterized notebook workflows.

Demonstrates data validation, transformation, and Delta Lake writes.

Key Features:

Reusable pipeline templates

Checkpointing for incremental processing

Config-driven table and path definitions

2. Spark Structured Streaming

Description:
Demonstrates real-time data processing using Spark Structured Streaming.

Reads from JSON, CSV, or Delta sources.

Performs transformations and aggregations.

Writes results to Delta tables on a Standard cluster with checkpointing.

Key Features:

Trigger-based micro-batch processing

Handles schema evolution and late-arriving data

3. Autoloader Structured Streaming

Description:
Demonstrates cloud-optimized streaming ingestion using Databricks Autoloader.

Automatically detects new files in a cloud storage location.

Scales efficiently for high-throughput streaming workloads.

Key Features:

Schema inference and evolution

Automatic checkpointing

Can run on serverless or standard clusters

Demonstrates best practices for Delta Lake streaming writes


Prerequisites:

Databricks workspace with Standard or Serverless clusters

Python 3.x / PySpark 3.x

Delta Lake

Cloud storage access (Azure Data Lake, AWS S3, or DBFS mounts)
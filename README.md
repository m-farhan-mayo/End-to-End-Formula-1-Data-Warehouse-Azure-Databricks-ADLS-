# End-to-End-Formula-1-Data-Warehouse-Azure-Databricks-ADLS

This repository contains a complete, end-to-end data engineering project that builds a Formula 1 Data Warehouse using Azure Databricks and Azure Data Lake Storage (ADLS).

The project demonstrates the entire data lifecycle, from initial environment setup and security to raw data ingestion, multi-stage transformations (Medallion Architecture), incremental loading, and final analysis.

It is a comprehensive reference for data engineering best practices on the Databricks platform, covering multiple data sources (circuits, drivers, races, pit stops, etc.) and culminating in analytics-ready tables for BI reporting.

Key Concepts & Project Recall (File Breakdown)
This project is organized into logical modules that represent a complete data engineering workflow:

set-up (Environment Configuration)

Purpose: This is the initial one-time setup. It contains all the different methods for securely connecting Azure Databricks to Azure Data Lake Storage.

Recall: You explored:

Access_adls_using_access_key.py: The direct (but less secure) method.

Access_adls_using_SAS_Token.py: Using a temporary, expiring token.

Access_adls_using_Service_Principal.py: The production-standard, automated way.

Mounting_adls_using_Service_Principal.py: Using a Service Principal to mount ADLS storage directly into the Databricks File System (DBFS).

Explore_dbutils_seret_utility.py: How to properly store and retrieve secrets (like keys) from Azure Key Vault using dbutils.secrets.get().

raw (Database Setup)

Purpose: Contains the DDL (CREATE TABLE, CREATE DATABASE) scripts to create the initial raw database.

Injection (Bronze Layer)

Purpose: This module is responsible for ingesting all the raw source files into the Bronze layer.

Recall: You built a separate, parameterized ingestion script for each data source (e.g., Injection_circuit_file.py, Injection_Race_File.py, Injection_Driver_File.py, etc.). The Injection All Files.py notebook was likely an orchestrator that ran all the other notebooks.

trans (Silver & Gold Layers)

Purpose: This is the core transformation logic.

Recall: calculate_race_result.py reads from all the various "Bronze" tables (drivers, circuits, races, etc.), joins them together, applies business logic, and creates the final, rich Gold table: race_results.

analysis (BI & Analytics)

Purpose: The final step. This contains the SQL queries you would run for analytics.

Recall: dominint_drivers.sql is a sample query that runs on the Gold race_results table to find the most successful drivers.

Incremental_load (Advanced Pattern)

Purpose: This module demonstrates a more advanced data loading pattern, showing how to process only new or changed data instead of reloading the entire dataset every time.

includes (Utilities & Best Practices)

Purpose: This folder contains reusable code to keep the project clean (DRY - Don't Repeat Yourself).

Recall:

Configuration.py: A central file to store all paths, table names, and other variables.

common_functions.py: A library of helper functions (e.g., add_ingestion_date()) that are imported and used by many different notebooks.

demo (Learning & Exploration)

Purpose: A sandbox for learning and testing specific Databricks features.

Recall: You have demos for basic DataFrame operations (filter_demo.py, join_demo.py), Spark SQL (sql_temp_view_demo.py), and fundamental Delta Lake commands (delta_lake_demo.py).

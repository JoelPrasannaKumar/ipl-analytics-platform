# 🏏 Enterprise IPL Analytics & ML Platform

An end-to-end Enterprise Data Platform built on Databricks using the Medallion Architecture (Bronze, Silver, Gold). This project processes raw IPL data into a clean, optimized format for BI consumption, and features an integrated Machine Learning pipeline to predict match outcomes.

## 🚀 Key Technologies
* **Databricks Serverless Compute**: For scalable data processing.
* **Apache Spark (PySpark & Spark SQL)**: For massive parallel data transformation and aggregation.
* **Delta Lake**: Ensuring ACID compliance, data versioning (Time Travel), and blazing-fast queries with `ZORDER` optimizations.
* **Unity Catalog**: Managing Data Governance, Role-Based Access Control (RBAC), and centralized metadata.
* **Machine Learning**: `scikit-learn` (Random Forest Classifier).
* **MLflow**: Experiment tracking and Model Registry integration.

## 🏗️ Architecture Flow
1. **Bronze Layer (Raw Ingestion)**: Ingests raw CSV data into Unity Catalog Volumes, adding mandatory audit metadata (`ingestion_ts`, `source_file`) without modifying the original data.
2. **Silver Layer (Cleaned & Conformed)**: Enforces strict data quality rules (e.g., valid overs, non-negative runs) and filters out abandoned matches to create a trusted source of truth.
3. **Gold Layer (Business Analytics)**: Uses complex Spark SQL aggregations to create BI-ready fact tables (`fact_match_summary`, `fact_player_performance`), heavily optimized for fast Dashboard querying.
4. **Data Science (MLflow)**: Leverages the pristine Gold layer data to train a Random Forest model predicting match winners, automatically logging parameters, metrics, and models to the Unity Catalog Model Registry.

## 📊 Setup & Usage
All code is consolidated in the `project.ipynb` Databricks notebook. 
To run this project:
1. Upload the `matches.csv` and `deliveries.csv` to a Databricks Unity Catalog Volume.
2. Import the `project.ipynb` Notebook into your Databricks Workspace.
3. Run the cells sequentially to execute the full pipeline from raw data to registered ML model.

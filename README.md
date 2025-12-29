# 🎬 End-to-End Azure Data Engineering Pipeline: MovieLens Analysis

![Project Status](https://img.shields.io/badge/Status-Completed-success)
![Tech Stack](https://img.shields.io/badge/Azure-Databricks-blue)
![Language](https://img.shields.io/badge/Python-PySpark-yellow)

## 📊 Project Overview
This project implements a scalable data engineering pipeline on **Microsoft Azure** to analyze the MovieLens dataset. The goal was to build a secure, cloud-native solution that ingests raw data, transforms it using **PySpark** on **Databricks**, and derives actionable insights about movie popularity and user ratings.

**Key Outcome:** Analyzed 100,000+ ratings to identify the highest-rated movies of all time, visualizing the results for business stakeholders.

## 🖼️ Analysis Result
*Output from the Gold Layer visualization:*

![Top Rated Movies Chart](chart.png)

---

## 🏗️ Architecture & Workflow
The pipeline follows the **Medallion Architecture** (Bronze → Silver → Gold) to ensure data quality and organization.



### 1️⃣ Bronze Layer (Ingestion & Extraction)
* **Security:** Configured **SAS Token (Shared Access Signature)** for secure, temporary access to Azure Data Lake Gen2 (ADLS), replacing the deprecated "Mounting" method.
* **Ingestion:** Ingested compressed raw data (`.zip`) from Azure Storage.
* **Extraction:** Implemented a shell-based logic to unzip files on the Databricks driver and re-upload extracted CSVs to the Data Lake.

### 2️⃣ Silver Layer (Transformation)
* **Schema Enforcement:** Loaded raw CSVs into Spark DataFrames with defined schemas.
* **Data Cleaning:** Converted Unix timestamps into human-readable `Date` formats using PySpark functions.
* **Handling:** Processed "Movies" and "Ratings" tables independently.

### 3️⃣ Gold Layer (Aggregation & Business Logic)
* **Join Logic:** Merged the Movies and Ratings datasets on `movieId`.
* **Aggregation:** Calculated the **Average Rating** and **Total Vote Count** per movie.
* **Filtering:** Applied a threshold (>50 votes) to filter out statistical outliers and focus on statistically significant data.

---

## 🛠️ Tech Stack
* **Cloud Platform:** Microsoft Azure
* **Storage:** Azure Data Lake Storage Gen2 (ADLS)
* **Compute:** Azure Databricks (Spark Cluster)
* **Language:** Python (PySpark)
* **Security:** SAS Tokens (Direct Access)

## 🚀 Key Learnings & Challenges
* **Security First:** Moving away from `dbutils.fs.mount()` to Direct Access via SAS Tokens to adhere to modern security best practices.
* **Handling Zipped Data:** Solved the limitation of Spark not reading zipped files natively in object storage by implementing a local-driver extraction pattern.
* **Optimization:** Used Spark's lazy evaluation and optimized transformations (narrow vs. wide) for efficient processing.

## 📈 Future Scope
* **Automation:** Orchestrate the notebook using **Azure Data Factory (ADF)** for daily runs.
* **Delta Lake:** Convert file formats to **Delta** tables to enable ACID transactions and "Time Travel."
* **Sentiment Analysis:** Use NLP to analyze user tags and reviews for deeper insights.

---
*Author: Sugam Dewan*

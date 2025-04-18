# Student Depression Data Pipeline (India) – Medallion Architecture with Delta Lake

## 📝 Project Overview

This project demonstrates how to implement a **Delta Lake Medallion Architecture** using PySpark to process, clean, and enrich raw data about **student depression in India**. The pipeline ingests data stored in an **S3 bucket**, transforms it through Bronze, Silver, and Gold layers, and stores it as Delta tables for analytics readiness.

---

## 📁 Data Source

The dataset used contains anonymized information about students across various cities in India, including:
- Academic & work pressure
- Sleep habits
- CGPA
- Dietary and mental health indicators
- Suicidal thoughts and depression flags

The file was initially stored in an **AWS S3 bucket** in CSV format.

---

## 🏗️ Architecture Overview

### 🔸 Bronze Layer – Raw Ingest
- Loaded the CSV file from the S3 bucket using a defined schema.
- Added metadata columns: `load_date` and `source_file_name`.
- Saved the ingested DataFrame as a **Delta table** in the `bronze` database.
  
### ⚙️ Silver Layer – Data Cleaning & Standardization
- Trimmed and standardized all string fields (e.g., lowercased 'Yes'/'No').
- Cleaned up Sleep_Duration formatting.
- Replaced yes/no flags with boolean indicators.
- Removed rows with invalid or null values (e.g., age outliers, null CGPA).
- Added processed_date for traceability.

### 🥇 Gold Layer – Feature Engineering & Business Logic
- Created derived columns for Overall_Stress, Total_Satisfaction, and Mental_Health_Risk_Flag.
- Categorized Sleep_Quality based on reported hours.
- Labeled records as "Depressed" or "Not Depressed".
- Added a gold_processed_date timestamp for audit purposes.

# 🍽️ Restaurant Inspection Data ETL Pipeline

This project demonstrates a full ETL (Extract, Transform, Load) pipeline for restaurant and food establishment inspection datasets from two major U.S. cities: **Dallas** and **Chicago**. The processed data is ultimately stored in a dimensional model and visualized using Power BI.

---

## 🔍 1. Extraction

The datasets used in this project were sourced from the open data portals of:

- **Dallas**: *Restaurant and Food Establishment Inspections*  
- **Chicago**: *Food Inspections*

For both cities:

- Raw datasets were ingested as delimited text files (`.csv`).
- **YData Profiling** was used to analyze data quality and generate HTML profile reports.
- These reports provided insights into data completeness, value distributions, and structure.

---

## 🔧 2. Transformation

The ETL workflows were built using **Talend Open Studio**. The key transformation steps included:

### 🗃️ Staging

- Input files were loaded into **MySQL staging tables** using:
  - `tFileInputDelimited`
  - `tMap`
  - `tDBOutput`

### 🔄 Normalization

- Nested fields like violations were normalized using `tNormalize`.
- Violations were split into individual records for proper modeling.

### 📊 Aggregation & Mapping

- Used `tAggregateRow` to summarize violation scores.
- Multiple `tMap` components were used to transform and route data into appropriate dimension and fact tables.

### 🧱 Dimensional Modeling

Created a star schema with the following tables:

- `address_dim`
- `facility_dim`
- `dim_date`
- `dim_violations`
- `fact_inspection`

Refer to Talend tMap screenshots and ER diagram for the exact data flow.

---

## 📥 3. Loading

The transformed and cleaned data was loaded into a **MySQL data warehouse**.

### 🧩 Schema Overview

- `address_dim`: Stores address-related fields including geolocation.
- `facility_dim`: Facility metadata like name, license, and type.
- `dim_date`: Temporal breakdown into day, month, year.
- `dim_violations`: Expanded list of all recorded violations.
- `fact_inspection`: Central fact table linking all dimensions, storing results and scores.

> 💡 All relevant DDL scripts are provided in the `/etl/sql/ddl_scripts.sql` file.

---

## 📊 Visualization

- **Power BI dashboards** were built to visualize insights such as:
  - Violation distribution over time
  - Risk categorization by location
  - Facility-wise inspection history
  - Total violation scores

Screenshots of the dashboards can be found in the `/dashboards/powerbi_screenshots/` directory.

---




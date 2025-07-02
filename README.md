```
# Maji Ndogo Water Access Project: Unveiling the Crisis through Data

## Overview
This repository contains the data analysis project focused on understanding and addressing the water crisis in Maji Ndogo. The project leverages a comprehensive dataset of water source visits, quality assessments, and employee activities to identify patterns, clean data, and derive actionable insights.

The work is structured into two main phases:
1.  **Phase 1: Initial Data Exploration & Quality Assessment (Maji Ndogo Part 1)**
    * Familiarization with foundational tables and their interconnections.
    * Initial assessment of data quality and identification of anomalies.
    * Basic analytical queries to understand existing conditions.
2.  **Phase 2: Data Cleaning, Deeper Analysis & Clustering (Maji Ndogo Part 2)**
    * Extensive data cleaning and transformation to ensure data integrity.
    * Detailed analysis of employee performance and location-based patterns.
    * Preparation for clustering techniques to uncover broader narratives and hidden correlations related to water access and quality.

## 📌 Objectives

The primary objectives of this project are to:

* **Understand Data Structure:** Gain a deep understanding of the Maji Ndogo water services database schema and relationships between tables.
* **Ensure Data Quality:** Identify and rectify inconsistencies, missing information, and erroneous entries across various tables (e.g., employee contact details, water source descriptions).
* **Analyze Water Sources:** Categorize and assess the distribution and types of water sources used by the population.
* **Investigate Operations:** Examine field worker visit patterns, identify anomalies, and evaluate their impact on data reliability and operational efficiency.
* **Assess Water Quality:** Analyze subjective quality scores and pollution data to pinpoint critical water quality issues.
* **Identify Key Areas for Intervention:** Use data-driven insights to recommend strategic interventions for improving water access and quality in Maji Ndogo.
* **Lay Foundation for Advanced Analytics:** Prepare cleaned and structured data for potential future use in clustering, predictive modeling, and dashboard reporting.

## 📂 Project Structure

```

.
├── data/
│   └── queue\_time\_for\_days\_and\_hours.xlsx - visits.csv  \# Cleaned/Processed CSV data related to visits
├── notebooks/
│   └── Integrated project Clustering data to unveil Maji Ndogo's water crisis.ipynb \# Jupyter Notebook with all SQL queries and analysis
└── README.md                                           \# This overview file

```

## 📊 Key Analyses & Insights Covered (with SQL Focus)

Throughout this project, we've executed various SQL queries and conducted analyses, including:

* **Database Familiarization:** Initial `SELECT * LIMIT X` queries to understand `location`, `water_source`, `visits`, and `well_pollution` tables.
* **Water Source Overview:** Using `SELECT DISTINCT type_of_water_source` to identify unique water access methods.
* **Visit Pattern Analysis (`visits` table):**
    * Identifying records with `visit_count > 1` and `time_in_queue != 0` to spot unusual activities.
    * Detecting potential data entry errors where `time_in_queue = 0` but `visit_count > 1`.
    * Aggregating visit counts per `location_id` using `COUNT()` and `GROUP BY` to identify high-activity areas.
* **Water Quality Anomalies (`water_quality` table):**
    * Pinpointing inconsistent records, such as `subjective_quality_score = 10` (home taps) with `visit_count > 1`, suggesting data integrity issues.
* **Data Cleaning - `employee` table:**
    * **Email Address Generation:** Used `CONCAT()`, `LOWER()`, and `REPLACE()` functions to create `employee_email` from `employee_name` and update the table.
    * **Phone Number Cleaning:** Employed `TRIM()` to remove extraneous spaces and `CONCAT()` with a `WHERE LIKE` clause to fix missing '+' prefixes for specific country codes (e.g., '25%').
* **Employee Performance & Location Analysis:**
    * Counting employees per `town_name` using `COUNT()` and `GROUP BY`.
    * Identifying top-performing employees (by `number_of_locations_visited`) using `COUNT()`, `GROUP BY`, `ORDER BY`, and `LIMIT`, and integrating this logic with `WITH` (CTE) clauses and `JOIN`s to retrieve full employee details (name, email, phone).
* **Understanding Data Interpretation:** Addressed specific scenarios, such as the misleading average of people sharing a tap, to highlight the importance of understanding data collection methodologies.
* **water source Analysis:**
    * How many people did we survey in total?
    * How many wells, taps and rivers are there?
    * What is the average number of people that are served by each water source?
    * How many people are getting water from each type of source?
* **queue time analysis on shared taps:** queue time was analysed for all day of the weeks for each of hours in a single day. Final summary is given on the notebokk based on the result of the analysis.
## 💡 Tools Used

* **SQL (with Jupyter Notebook / Python integration):** For all data querying, cleaning, transformation, and analysis.
* **Jupyter Notebook:** For an interactive environment to write and execute SQL, document findings.
* **Microsoft Excel / CSV:** For the purpose of showing queue times with visualization and pivot table.

## 📬 Contact

Created and maintained by **Henock**.

Feel free to reach out with any questions or feedback!
```
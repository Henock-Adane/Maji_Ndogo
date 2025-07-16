
# Maji Ndogo Water Access Project: Unveiling the Crisis through Data

## Overview

This repository contains the data analysis project focused on understanding and addressing the water crisis in Maji Ndogo. The project leverages a comprehensive dataset of water source visits, quality assessments, and employee activities to identify patterns, clean data, and derive actionable insights.

The work is structured into multiple phases:

1. **Phase 1: Initial Data Exploration & Quality Assessment (Maji Ndogo Part 1)**
   - Familiarization with foundational tables and their interconnections.
   - Initial assessment of data quality and identification of anomalies.
   - Basic analytical queries to understand existing conditions.

2. **Phase 2: Data Cleaning, Deeper Analysis & Clustering (Maji Ndogo Part 2)**
   - Extensive data cleaning and transformation to ensure data integrity.
   - Detailed analysis of employee performance and location-based patterns.
   - Preparation for clustering techniques to uncover broader narratives and hidden correlations related to water access and quality.

3. **Phase 3: Weaving the Data Threads of Maji Ndogo’s Narrative (Maji Ndogo Part 3)**
   - Validate the integrity of subjective water quality scores submitted by employees.
   - Identify potential data manipulation or systemic issues.
   - Use SQL to trace inconsistencies to specific employees and locations.

4. **Phase 4: From Analysis to Action (Maji Ndogo Part 4)**
   - Combine survey, water quality, and pollution data into a unified view for planning.
   - Summarize water source conditions by province and town.
   - Recommend specific engineering interventions for contaminated or inadequate sources.
   - Create and populate a `Project_progress` table to track repair initiatives with conditional SQL logic.
   - Assign improvements based on contamination type, water source condition, and queue time patterns.

## 📌 Objectives

The primary objectives of this project are to:

- **Understand Data Structure:** Gain a deep understanding of the Maji Ndogo water services database schema and relationships between tables.
- **Ensure Data Quality:** Identify and rectify inconsistencies, missing information, and erroneous entries across various tables (e.g., employee contact details, water source descriptions).
- **Analyze Water Sources:** Categorize and assess the distribution and types of water sources used by the population.
- **Investigate Operations:** Examine field worker visit patterns, identify anomalies, and evaluate their impact on data reliability and operational efficiency.
- **Assess Water Quality:** Analyze subjective quality scores and pollution data to pinpoint critical water quality issues.
- **Identify Key Areas for Intervention:** Use data-driven insights to recommend strategic interventions for improving water access and quality in Maji Ndogo.
- **Lay Foundation for Advanced Analytics:** Prepare cleaned and structured data for potential future use in clustering, predictive modeling, and dashboard reporting.

## 📂 Project Structure

```
├── data/
│   ├── queue_time_for_days_and_hours.xlsx
│   └── visits.csv                      # Cleaned/Processed CSV data related to visits
├── notebooks/
│   └── Integrated_project_Clustering_data_to_unveil_Maji_Ndogo's_water_crisis.ipynb  # Jupyter Notebook with all SQL queries and analysis
│   └── Integrated_project_Weaving_the_data_threads_of_Maji_Ndogos_narrative.ipynb     # Audit investigation notebook
│   └── Charting_the_course_for_Maji_Ndogo's_water_future.ipynb                                           # Repair plan and engineering actions
└── README.md                          # This overview file
```

## 📊 Key Analyses & Insights Covered (with SQL Focus)

Throughout this project, we've executed various SQL queries and conducted analyses, including:

- **Database Familiarization:** Initial `SELECT * LIMIT X` queries to understand `location`, `water_source`, `visits`, and `well_pollution` tables.
- **Water Source Overview:** Using `SELECT DISTINCT type_of_water_source` to identify unique water access methods.

### Visit Pattern Analysis (`visits` table):
- Identifying records with `visit_count > 1` and `time_in_queue != 0` to spot unusual activities.
- Detecting potential data entry errors where `time_in_queue = 0` but `visit_count > 1`.
- Aggregating visit counts per `location_id` using `COUNT()` and `GROUP BY` to identify high-activity areas.

### Water Quality Anomalies (`water_quality` table):
- Pinpointing inconsistent records, such as `subjective_quality_score = 10` (home taps) with `visit_count > 1`, suggesting data integrity issues.

### Data Cleaning - `employee` table:
- **Email Address Generation:** Used `CONCAT()`, `LOWER()`, and `REPLACE()` functions to create `employee_email` from `employee_name` and update the table.
- **Phone Number Cleaning:** Employed `TRIM()` to remove extraneous spaces and `CONCAT()` with a `WHERE LIKE` clause to fix missing '+' prefixes for specific country codes (e.g., `'25%'`).

### Employee Performance & Location Analysis:
- Counting employees per `town_name` using `COUNT()` and `GROUP BY`.
- Identifying top-performing employees (by `number_of_locations_visited`) using `COUNT()`, `GROUP BY`, `ORDER BY`, and `LIMIT`, and integrating this logic with `WITH` (CTE) clauses and `JOIN`s to retrieve full employee details (name, email, phone).

### Understanding Data Interpretation:
- Addressed specific scenarios, such as the misleading average of people sharing a tap, to highlight the importance of understanding data collection methodologies.

### Water Source Analysis:
- How many people did we survey in total?
- How many wells, taps, and rivers are there?
- What is the average number of people that are served by each water source?
- How many people are getting water from each type of source?

### Queue Time Analysis on Shared Taps:
- Queue time was analyzed for all days of the week and across each hour in a single day.
- Final summary is provided in the notebook based on the results.
### Adding Auditor Report and Evaluation
- **Import Auditor Report:**
  - Structured the `auditor_report.csv` into a SQL table.
  - Fields: `location_id`, `true_water_source_score`, `type_of_water_source`, `statements`.

- **Score Comparison (Surveyor vs. Auditor):**
  - Joined the auditor table with the internal `visits` and `water_quality` tables.
  - Compared each surveyor’s `subjective_quality_score` with the auditor’s `true_water_source_score`.

- **Error Detection & Isolation:**
  - Found that 102 out of 1620 reviewed records contained mismatches.
  - Verified that water source types were still consistent across datasets.

- **Employee Accountability:**
  - Identified employees responsible for mismatched data by joining `assigned_employee_id`.
  - Created a view `Incorrect_records` to streamline further analysis.

- **Error Frequency Analysis:**
  - Counted how many mismatches each employee submitted.
  - Highlighted those with above-average error counts using CTEs (`error_count`, `suspect_list`).

- **Corruption Red Flags (Qualitative Review):**
  - Queried auditor-provided `statements` to identify references to potential bribery (e.g., “cash”).
  - Confirmed that only a small group of employees appeared repeatedly in both numeric and narrative inconsistencies.

### Final Outcome

- 4 employees were flagged for further investigation:
  - **Above-average error counts**
  - **Recurring mentions of bribes or irregularities in statements**
- This analysis helps leadership take targeted action to restore data reliability and improve accountability in Maji Ndogo’s water service program.

### Final Repair Plan Logic (Maji Ndogo Part 4)

- **Created `combined_analysis_table`** by joining `visits`, `location`, `water_source`, and `well_pollution`, filtered to `visit_count = 1`.

- **Province- and Town-level summaries**:
  - Calculated percentage of people using each source type per region.
  - Identified hotspots needing infrastructure upgrades or new water sources.

- **Created `Project_progress` table** to manage intervention projects:
  - Tracks source ID, location, proposed fix, and completion status.

- **Populated `Project_progress` using conditional SQL:**
  - **Wells**:
    - `Contaminated: Biological` → `Install UV and RO filter`
    - `Contaminated: Chemical` → `Install RO filter`
  - **Shared taps** with `queue_time >= 30` → `Install X taps nearby`
  - **Tap in home broken** → `Diagnose local infrastructure`
  - **Rivers** → `Drill well`

- **Used `UPDATE` statements with `CASE` and `JOINs` or subqueries** to set improvements based on logic described above.

## 💡 Tools Used

- **SQL (with Jupyter Notebook / Python integration):** For all data querying, cleaning, transformation, and analysis.
- **Jupyter Notebook:** For an interactive environment to write and execute SQL, document findings.
- **Microsoft Excel / CSV:** For visualizing queue times with charts and pivot tables.

## 📬 Contact

Created and maintained by **Henock**.

Feel free to reach out with any questions or feedback!

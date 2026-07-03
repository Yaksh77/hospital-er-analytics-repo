# 🏥 Hospital ER Patient Analytics Dashboard

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![Excel/CSV](https://img.shields.io/badge/Data%20Format-CSV-217346?style=for-the-badge&logo=microsoftexcel&logoColor=white)
![DAX](https://img.shields.io/badge/DAX-Measures-blue?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge)

A Power BI business intelligence project analyzing Emergency Room (ER) patient admissions, wait times, satisfaction scores, and department referrals for a hospital network — built to help hospital administrators monitor patient flow and service quality at a glance.

---

## 📋 Table of Contents

- [Project Overview](#-project-overview)
- [Business Problem](#-business-problem)
- [Dataset Overview](#-dataset-overview)
- [Tech Stack](#-tech-stack)
- [Dashboard Overview](#-dashboard-overview)
- [Dashboard Pages](#-dashboard-pages)
- [Key Metrics Tracked](#-key-metrics-tracked)
- [Business Insights](#-business-insights)
- [Repository Structure](#-repository-structure)
- [How to Use](#-how-to-use)
- [Future Improvements](#-future-improvements)
- [Author](#-author)

---

## 📊 Project Overview

This project turns raw Emergency Room admission records into an interactive Power BI dashboard. It tracks how many patients are being seen, how long they wait, how satisfied they are, and which departments they're referred to — broken down by time period, demographics, and admission status.

## 🎯 Business Problem

Hospital administrators need a fast, visual way to answer questions like:

- How many patients are coming through the ER, and is that trending up or down month over month?
- Are patients being seen within an acceptable wait-time window (30 minutes)?
- How does patient satisfaction compare across demographics and departments?
- Which departments receive the most referrals, and where is capacity strained?

This dashboard consolidates that information into three focused report pages instead of manual spreadsheet reporting.

## 🗂️ Dataset Overview

| Detail | Value |
|---|---|
| File | `Dataset/Hospital ER_Data.csv` |
| Rows | 9,216 patient records |
| Columns | 12 |
| Date Range | April 2023 – October 2024 |
| Grain | One row per patient admission event |
| Data Source | Unable to determine from the available project files (no source/provenance file included; dataset appears to be a synthetic/practice ER dataset commonly used for BI portfolio projects) |

### Data Dictionary

| Column | Type | Description | Missing Values |
|---|---|---|---|
| `Patient Id` | Text | Unique patient identifier (formatted like an SSN) | 0 |
| `Patient Admission Date` | Datetime | Date and time the patient was admitted (`DD-MM-YYYY HH:MM`) | 0 |
| `Patient First Inital` | Text | Patient's first initial | 0 |
| `Patient Last Name` | Text | Patient's last name | 0 |
| `Patient Gender` | Text | `M`, `F`, or `NC` (not classified) | 0 |
| `Patient Age` | Integer | Patient age in years (range: 1–79) | 0 |
| `Patient Race` | Text | Self-identified race/ethnicity (7 categories) | 0 |
| `Department Referral` | Text | Department the patient was referred to (7 departments) | 5,400 (58.6%) — likely means "not referred / stayed in ER" |
| `Patient Admission Flag` | Boolean | Whether the patient was formally admitted (`TRUE`/`FALSE`) | 0 |
| `Patient Satisfaction Score` | Float | Satisfaction rating, 0–10 scale | 6,699 (72.7%) — survey not completed by most patients |
| `Patient Waittime` | Integer | Wait time in minutes (range: 10–60) | 0 |
| `Patients CM` | Integer (flag) | Unable to determine exact business meaning from available files (binary flag, 0/1; appears in only 5.2% of records as `1`) | 0 |

**Data quality notes:**
- No duplicate records were found in the dataset.
- `Department Referral` and `Patient Satisfaction Score` contain a large proportion of missing values, which appears to be expected (not every patient is referred to a specialist department, and not every patient completes a satisfaction survey) rather than a data quality defect — this should be confirmed with the data owner if the dataset is used beyond a portfolio context.

## 🛠️ Tech Stack

![Power BI](https://img.shields.io/badge/Power%20BI%20Desktop-F2C811?style=flat-square&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-004E8C?style=flat-square)
![CSV](https://img.shields.io/badge/CSV-217346?style=flat-square)

| Layer | Tool |
|---|---|
| Data Storage | CSV |
| Data Modeling & Transformation | Power Query (within Power BI Desktop) |
| Measures / Calculations | DAX |
| Visualization | Power BI Desktop (`.pbix`) |

> No SQL scripts, Python notebooks, or cloud/database platforms were found in this project — this repository is a pure Power BI (Power Query + DAX) analytics project.

## 📈 Dashboard Overview

The report contains **3 pages** built in Power BI Desktop, all connected to the same ER dataset and a supporting Date table, with consistent slicers and navigation buttons across pages.

## 🖼️ Dashboard Pages

### 1. Monthly View
![Monthly View](Dashboard%20Images/monthly_view.jpg)

Month-by-month breakdown of ER activity: patient volume trend, average wait time, average satisfaction score, admission status split, gender/race breakdown, and patients seen by day and hour — filterable by month.

### 2. Consolidated View
![Consolidated View](Dashboard%20Images/consolidated_view.jpg)

A full-period rollup of the same KPIs (no month filter applied) plus additional breakdowns by age group and department referral, giving a single-page executive summary.

### 3. Patient Details
![Patient Details](Dashboard%20Images/patient_details.jpg)

A drill-through/detail table page listing individual patient-level records for ad-hoc lookups and auditing.

*(Full-resolution screenshots are available in the [`Dashboard Images/`](./Dashboard%20Images) folder.)*

## 📌 Key Metrics Tracked

Based on the fields referenced throughout the report visuals:

- **No. of Patients** — total patient count
- **Avg. Wait Time** — average `Patient Waittime`
- **Avg. Satisfaction Score** — average `Patient Satisfaction Score`
- **% of Patients Seen Within 30 Min** — share of visits with wait time ≤ 30 minutes
- **% of Patients by Gender**
- **No. of Patients Referred / No. of Patients Referred by department**
- **Patient Admission Status** (admitted vs. not admitted)
- **No. of Patients by Day and Hour**
- **Age Group** and **Waittime Interval / Waittime Status** — binned/calculated fields used for grouping

> Exact DAX formulas could not be extracted from the compressed Power BI data model file — see [`Documentation/DAX_Measures.md`](./Documentation/DAX_Measures.md) for the full list of identified measures/calculated columns and instructions for documenting their formulas.

## 💡 Business Insights

The following are descriptive observations directly computed from the underlying dataset (not the dashboard's internal logic, which uses its own binning):

- ER volume in the dataset spans **April 2023 – October 2024**, across **9,216 admissions**.
- **40.7%** of patients were seen within 30 minutes; the overall average wait time is **35.3 minutes** (range 10–60 minutes).
- Admissions are almost evenly split — **4,612 patients (50.0%)** were formally admitted (`Patient Admission Flag = TRUE`) vs. **4,604 (50.0%)** not admitted.
- Gender distribution: **4,705 male**, **4,487 female**, **24 not classified**.
- Of patients with a recorded department referral, **General Practice (1,840)** and **Orthopedics (995)** receive the highest volumes; **Renal (86)** and **Gastroenterology (178)** receive the fewest.
- **58.6%** of records have no department referral recorded, and **72.7%** have no satisfaction score recorded — worth flagging to stakeholders if survey completion or referral capture is a process metric of interest.

## 🗃️ Repository Structure

```
hospital-er-analytics/
│
├── Dataset/
│   └── Hospital ER_Data.csv          # Raw ER patient-level data (9,216 rows x 12 columns)
│
├── Power BI/
│   └── Dashboards.pbix               # Power BI report (3 pages, DAX measures, Power Query model)
│
├── Dashboard Images/
│   ├── monthly_view.jpg              # Screenshot: Monthly View page
│   ├── consolidated_view.jpg         # Screenshot: Consolidated View page
│   └── patient_details.jpg           # Screenshot: Patient Details page
│
├── Documentation/
│   ├── Dataset_README.md             # Data dictionary & data quality notes
│   ├── PowerBI_README.md             # Dashboard pages, visuals, and layout documentation
│   └── DAX_Measures.md               # Identified measures/calculated columns (placeholders for formulas)
│
├── .gitignore
├── LICENSE
└── README.md
```

## ▶️ How to Use

1. Clone or download this repository.
2. Open `Power BI/Dashboards.pbix` in [Power BI Desktop](https://www.microsoft.com/en-us/power-platform/products/power-bi/desktop) (free).
3. If prompted, point the data source back to `Dataset/Hospital ER_Data.csv` on your local machine.
4. Use the slicers on each page to filter by month, gender, or department.

No installation beyond Power BI Desktop is required — there is no database, API, or cloud service dependency in this project.

## 🔭 Future Improvements

- Document the exact DAX formulas behind each measure (see placeholder file) directly from Power BI Desktop's Model view.
- Investigate and document the business meaning of the `Patients CM` column with the data owner.
- Add a Power Query / data-cleaning step log describing how missing `Department Referral` and `Patient Satisfaction Score` values are handled in the model.
- Publish the report to the Power BI Service and link a live/read-only view here.
- Add row-level security (RLS) if this were extended to a multi-hospital or multi-department deployment.

## 👤 Author

*Add your name, LinkedIn, and portfolio link here.*

---
*This README was generated from a direct inspection of the project's dataset, Power BI report layout, and dashboard screenshots. No features, metrics, or dashboards described above were invented — anything that could not be confirmed from the available files is explicitly marked as such.*

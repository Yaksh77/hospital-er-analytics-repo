# Dataset Documentation

## File

`Dataset/Hospital ER_Data.csv`

## Summary

| Metric | Value |
|---|---|
| Rows | 9,216 |
| Columns | 12 |
| Duplicate rows | 0 |
| Date range | 2023-04-01 to 2024-10-30 |
| Encoding | UTF-8 with BOM |

## Data Dictionary

| # | Column | Data Type | Example Value | Description | Missing | % Missing |
|---|---|---|---|---|---|---|
| 1 | `Patient Id` | Text | `145-39-5406` | Unique identifier per patient record | 0 | 0.0% |
| 2 | `Patient Admission Date` | Datetime (`DD-MM-YYYY HH:MM`) | `20-03-2024 08:47` | Date/time the patient was admitted to the ER | 0 | 0.0% |
| 3 | `Patient First Inital` | Text (1 char) | `H` | Patient's first initial | 0 | 0.0% |
| 4 | `Patient Last Name` | Text | `Glasspool` | Patient's last name | 0 | 0.0% |
| 5 | `Patient Gender` | Categorical | `M`, `F`, `NC` | Patient gender (`NC` = not classified) | 0 | 0.0% |
| 6 | `Patient Age` | Integer | `69` | Patient age in years (min 1, max 79) | 0 | 0.0% |
| 7 | `Patient Race` | Categorical (7 values) | `White` | Self-identified race/ethnicity | 0 | 0.0% |
| 8 | `Department Referral` | Categorical (7 values + blank) | `General Practice` | Department the patient was referred to, if any | 5,400 | 58.6% |
| 9 | `Patient Admission Flag` | Boolean | `TRUE` | Whether the patient was formally admitted | 0 | 0.0% |
| 10 | `Patient Satisfaction Score` | Float (0–10) | `9.0` | Patient satisfaction survey score | 6,699 | 72.7% |
| 11 | `Patient Waittime` | Integer (minutes) | `39` | Time waited before being seen (min 10, max 60) | 0 | 0.0% |
| 12 | `Patients CM` | Integer flag (0/1) | `0` | Unable to determine exact business meaning from available files | 0 | 0.0% |

## Categorical Value Breakdown

**Patient Gender**
| Value | Count |
|---|---|
| M | 4,705 |
| F | 4,487 |
| NC | 24 |

**Patient Race**
| Value | Count |
|---|---|
| White | 2,571 |
| African American | 1,951 |
| Two or More Races | 1,557 |
| Asian | 1,060 |
| Declined to Identify | 1,030 |
| Pacific Islander | 549 |
| Native American/Alaska Native | 498 |

**Department Referral**
| Value | Count |
|---|---|
| *(blank / not referred)* | 5,400 |
| General Practice | 1,840 |
| Orthopedics | 995 |
| Physiotherapy | 276 |
| Cardiology | 248 |
| Neurology | 193 |
| Gastroenterology | 178 |
| Renal | 86 |

**Patient Admission Flag**
| Value | Count |
|---|---|
| TRUE | 4,612 |
| FALSE | 4,604 |

## Numeric Summary

| Column | Min | 25% | Median | 75% | Max | Mean | Std Dev |
|---|---|---|---|---|---|---|---|
| Patient Age | 1 | 20 | 39 | 60 | 79 | 39.86 | 22.76 |
| Patient Waittime | 10 | 23 | 35 | 48 | 60 | 35.26 | 14.74 |
| Patient Satisfaction Score* | 0 | 2 | 5 | 8 | 10 | 4.99 | 3.14 |

*Calculated only on the 2,517 non-missing records (27.3% response rate).*

## Data Source

Unable to determine from the available project files. No data-source, README, or provenance file accompanied the raw CSV. The structure and formatting (synthetic patient names, uniform ID pattern, evenly-distributed random values) is consistent with a publicly available practice/portfolio dataset used for Power BI training rather than real clinical data — this should not be treated as PHI or used to represent real patients.

## Business Meaning

- Each row represents a single ER patient admission event.
- `Patient Admission Flag` distinguishes ER visits that resulted in formal hospital admission from those that did not.
- `Department Referral` captures where a patient was routed for further care, if any.
- `Patient Satisfaction Score` and `Patient Waittime` are the two primary service-quality metrics tracked on the dashboard.

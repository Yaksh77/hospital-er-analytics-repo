# Power BI Report Documentation

## File

`Power BI/Dashboards.pbix`

## Overview

The report contains **3 pages**, all built against a single data model consisting of:
- `Hospital ER_Data` (the source table, `Dataset/Hospital ER_Data.csv`)
- `Date Table` (a supporting date dimension table with `Date`, `Day Name`, `Month Name`, `Year`, and a `Month & Year` field, used for time-based filtering and the Date Hierarchy)

Navigation buttons (`actionButton` visuals) are present on each page for switching between report pages.

---

## Page 1 — Monthly View

![Monthly View](../Dashboard%20Images/monthly_view.jpg)

**Purpose:** Track ER performance for a single selected month.

**Visuals identified on this page:**
| Visual Type | Purpose |
|---|---|
| Slicer (x2) | Filter by month and other dimension(s) |
| Card (x4) | Headline KPI numbers (e.g., No. of Patients, Avg. Wait Time, Avg. Satisfaction Score) |
| Area Chart (x3) | Trend visuals over time |
| Bar Chart | Category comparison |
| Clustered Column Chart (x2) | Category comparison across groups |
| Clustered Bar Chart (x2) | Category comparison across groups |
| Donut Chart — "% of Patients Seen Within 30 Min" | Wait-time SLA performance |
| Donut Chart — "% of Patients by Gender" | Gender breakdown |
| Clustered Column Chart — "No. of Patients by Day and Hour" | Volume pattern by day/hour |
| Pivot Table — "Patient Admission Status" | Admitted vs. not-admitted breakdown |
| Pivot Table (unlabeled) | Supporting cross-tab detail |
| Image / Textboxes / Shapes | Branding and page layout elements |

---

## Page 2 — Consolidated View

![Consolidated View](../Dashboard%20Images/consolidated_view.jpg)

**Purpose:** Full-period (all months) executive rollup of the same KPIs as the Monthly View, plus additional breakdowns.

**Visuals identified on this page:**
| Visual Type | Purpose |
|---|---|
| Slicer | Filter (e.g., department or demographic) |
| Card (x4) | Headline KPI numbers |
| Column Chart (x4) | Category comparisons (e.g., by age group, department referral) |
| Bar Chart | Category comparison |
| Clustered Column Chart | Category comparison |
| Clustered Bar Chart (x2) | Category comparison |
| Donut Chart — "% of Patients Seen Within 30 Min" | Wait-time SLA performance |
| Donut Chart — "% of Patients by Gender" | Gender breakdown |
| Clustered Column Chart — "No. of Patients by Day and Hour" | Volume pattern by day/hour |
| Pivot Table — "Patient Admission Status" | Admitted vs. not-admitted breakdown |
| Pivot Table (unlabeled) | Supporting cross-tab detail |
| Image / Textboxes / Shapes | Branding and page layout elements |

---

## Page 3 — Patient Details

![Patient Details](../Dashboard%20Images/patient_details.jpg)

**Purpose:** Row-level lookup/detail table for individual patient records.

**Visuals identified on this page:**
| Visual Type | Purpose |
|---|---|
| Table (`tableEx`) | Patient-level detail grid |
| Slicer | Filter the detail table |
| Image / Textboxes / Shapes | Branding and page layout elements |

---

## Fields Referenced Across the Report

Extracted directly from the visual query definitions inside the report layout:

**From `Hospital ER_Data`:**
`Patient Id`, `Patient Full Name`, `Patient Gender`, `Patient Race`, `Patient Age`, `Patient Admin Date`, `Department Referral`, `Admission Status`, `Age Group`, `Avg. Satisfaction Score`, `Avg. Wait Time`, `No. of Patients`, `No. of Patients1`, `No. Of Patients Referred`, `No.of Patients Referred`, `Waittime Interval`, `Waittime Status`

**From `Date Table`:**
`Date`, `Day Name`, `Month Name`, `Year`, `Month & Year`, `Date Hierarchy`

Fields such as `Age Group`, `Admission Status`, `Waittime Interval`, `Waittime Status`, and the `No. of Patients...` variants appear to be **calculated columns or measures** built on top of the raw CSV columns (e.g., grouping `Patient Age` into bands, or `Patient Waittime` into SLA buckets). See [`DAX_Measures.md`](./DAX_Measures.md) for a placeholder list — the underlying DAX formulas could not be extracted from the compressed data model file and should be copied in directly from Power BI Desktop's Model view.

## Filters & Slicers

- Month/date slicer(s) on the Monthly View page.
- At least one additional slicer per page (exact field not extractable from the compressed model — confirm in Power BI Desktop).
- Cross-page navigation via action buttons on every page.

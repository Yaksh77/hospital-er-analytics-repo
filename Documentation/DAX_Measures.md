# DAX Measures & Calculated Columns

## ⚠️ Note on Extraction

The Power BI data model (`DataModel` inside `Dashboards.pbix`) is stored in Microsoft's compressed VertiPaq binary format, which cannot be safely parsed as plain text. As a result, the **exact DAX formulas** behind each measure/calculated column could not be extracted or verified from the files in this repository.

The list below contains the **field names actually referenced by the report's visuals** (extracted from the report layout), which represent real measures/calculated columns that exist in the model. Formulas are left as placeholders — copy the real expression from **Power BI Desktop → Model view → select the field → Formula bar** and paste it in below.

Do not treat the "Formula" cells as real DAX until filled in from the source file.

---

### No. of Patients

- **Formula:** `<paste from Power BI Desktop>`
- **Purpose:** Count of patient records (likely `COUNTROWS` or `COUNT` of `Patient Id`)
- **Business Use:** Headline KPI card on Monthly View and Consolidated View

### No. of Patients1 / No.of Patients Referred / No. Of Patients Referred

- **Formula:** `<paste from Power BI Desktop>`
- **Purpose:** Unable to determine from the available project files — likely variants of patient count filtered by referral status or used to avoid circular filter context in a specific visual
- **Business Use:** Referral volume tracking

### Avg. Wait Time

- **Formula:** `<paste from Power BI Desktop>`
- **Purpose:** Average of `Patient Waittime`
- **Business Use:** Headline KPI card; service-level tracking

### Avg. Satisfaction Score

- **Formula:** `<paste from Power BI Desktop>`
- **Purpose:** Average of `Patient Satisfaction Score`
- **Business Use:** Headline KPI card; patient experience tracking

### Admission Status

- **Formula:** `<paste from Power BI Desktop>`
- **Purpose:** Unable to determine exact logic — likely a calculated column mapping `Patient Admission Flag` (`TRUE`/`FALSE`) to a readable label (e.g., "Admitted" / "Not Admitted")
- **Business Use:** Drives the "Patient Admission Status" pivot table on both dashboard pages

### Age Group

- **Formula:** `<paste from Power BI Desktop>`
- **Purpose:** Unable to determine exact bucket boundaries — likely a calculated column grouping `Patient Age` into bands (e.g., 0–18, 19–35, 36–60, 60+)
- **Business Use:** Age-based demographic breakdown

### Waittime Interval / Waittime Status

- **Formula:** `<paste from Power BI Desktop>`
- **Purpose:** Unable to determine exact bucket boundaries — likely calculated columns grouping `Patient Waittime` into SLA bands, feeding the "% of Patients Seen Within 30 Min" donut chart
- **Business Use:** Wait-time SLA / service-level tracking

---

## How to Complete This Document

1. Open `Power BI/Dashboards.pbix` in Power BI Desktop.
2. Switch to **Model view** (or the **Data** pane in Report view).
3. Click each measure/calculated column listed above.
4. Copy the exact expression from the formula bar into the corresponding "Formula" line here.
5. Remove this note once all placeholders are filled in.

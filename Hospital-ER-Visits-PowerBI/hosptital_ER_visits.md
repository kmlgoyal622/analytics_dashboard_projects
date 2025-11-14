# Hospital Emergency Room Visits Dashboard (Power BI)

## 📌 Project Overview
This Power BI project analyzes **10,000+ Emergency Room (ER) visit records** to understand patient demographics, wait times, satisfaction scores, visit patterns, and referral behavior.  
The dashboard supports hospital workflow optimization, resource allocation, and patient experience improvement.

![Hospital ER Dashboard](Dashboard1.png)

---

## 🗂️ Data Sources
- `patients.csv` – Patient IDs, gender, age group, race  
- `visits.csv` – Visit date/time, wait time, satisfaction  
- `referrals.csv` – Referral department details  
- `heatmap_data.csv` – Hourly patient visit intensity  
- All files were cleaned using Power Query inside Power BI.

---

## 🔧 Data Engineering & Transformation (ETL)
Performed inside **Power Query**:
- Removed duplicates, standardized date formats.
- Extracted **Year, Month, Hour** from datetime fields.
- Merged tables based on `PatientID` and `VisitID`.
- Created custom columns for:
  - **Age Buckets (0–18, 19–65, 66+)**
  - **Wait Time Groups**
- Converted categorical fields into dimensional attributes.

---

## 🧠 Data Modeling (Star Schema)
A **Star Schema** was designed to improve performance and DAX efficiency:

### **Fact Table**
- `Fact_Visits`  
Contains visit-level metrics (wait time, visit date, satisfaction score, referral).

### **Dimension Tables**
- `Dim_Patient`  
- `Dim_Date`  
- `Dim_Race`  
- `Dim_Department`  

✔ Relationships created using **1:* cardinality**  
✔ Active relationship based on **VisitDate → DateKey**

---

## 📐 DAX Measures
Key measures developed:
```DAX
Total Patients = COUNT(Fact_Visits[VisitID])
Avg Wait Time = AVERAGE(Fact_Visits[WaitTime])
Avg Satisfaction = AVERAGE(Fact_Visits[Satisfaction])
Patients by Age = COUNTROWS(FILTER(Fact_Visits, Fact_Visits[AgeGroup] = "19-65"))
Referrals Count = COUNT(Fact_Visits[ReferralDept])

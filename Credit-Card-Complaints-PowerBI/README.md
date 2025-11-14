# Credit Card Complaints Analytics (Power BI)

## 📌 Project Overview
This Power BI dashboard provides insights into **86,000+ consumer credit card complaints**.  
It covers complaint trends, top issues, state-level patterns, and company response performance.

![Credit Card Complaints Dashboard](CreditCardDashboard.png)

---

## 🗂️ Data Sources
- `complaints.csv` – Complaint details (issue, date, state)
- `responses.csv` – Company response statuses
- `state_coordinates.csv` – For geographic mapping

Performed preprocessing using Power Query.

---

## 🔧 ETL & Data Preparation
- Null handling & anomaly detection  
- Standardized issue categories  
- Created `DateKey` (YYYYMMDD)  
- Extracted **Week, Month, Year**  
- Grouped complaint types & response categories

---

## 🧠 Data Modeling (Star Schema)
### Fact Table:
- `Fact_Complaints` – complaint details

### Dimensions:
- `Dim_Date`
- `Dim_Issue`
- `Dim_State`
- `Dim_Response`

Optimized with **bi-directional filtering OFF** for performance.

---

## 📐 DAX Measures
```DAX
Total Complaints = COUNT(Fact_Complaints[ComplaintID])
Rolling 12 Months = CALCULATE([Total Complaints], DATESINPERIOD(Dim_Date[Date], MAX(Dim_Date[Date]), -12, MONTH))
Closed % = DIVIDE([Closed Complaints], [Total Complaints])

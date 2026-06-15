# ✈️ Customer Loyalty Data Warehouse

> A complete **End-to-End Data Warehouse** solution for an airline customer loyalty program, built as part of the **NTI Hireready Data Engineering & Analysis Course**.

---

## 📌 Project Overview

This project implements a full **ETL pipeline** and **dimensional data model** to analyze customer flight activity, loyalty points, and enrollment behavior. The solution covers everything from raw data ingestion to interactive Power BI dashboards with 3 report pages.

---

## 🏗️ Architecture

```
Source Data (CSV Files)
        ↓
[ODS] Operational Data Store  →  Raw data loaded from source systems
        ↓
[STG] Staging Layer           →  Cleaned & standardized data
        ↓
[DWH] Data Warehouse          →  Star Schema ready for analytics
        ↓
[Power BI] Dashboard          →  Interactive reports & KPIs
```

---

## 🔄 ETL Pipeline (SSIS)

### ODS Layer — Data Ingestion
The ODS package loads raw source data using a **Sequence Container**:

```
Execute SQL Task
      ↓
   Calendar
      ↓
Customer Flight Activity
      ↓
Customer Loyalty History
```

### DWH Layer — Dimensional Loading
Dimensions are loaded in order to respect foreign key dependencies:

```
Dim_Date
   ↓
Dim_Customer
   ↓
Dim_Enrollment
   ↓
Dim_Gender
   ↓
Dim_Geography
   ↓
Dim_LoyaltyCard
   ↓
Fact_Table
```

---

## 🗂️ Data Model — Star Schema

### ⭐ Fact Table
| Column | Type | Description |
|--------|------|-------------|
| Fact_Id | int | Primary Key |
| DateKey | int | FK → Dim_Date |
| Id_Cus | int | FK → Dim_Customer |
| Total_Flights | int | Number of flights |
| Distance | int | Total distance flown (km) |
| Points_Accumulated | int | Loyalty points earned |
| Points_Redeemed | int | Loyalty points redeemed |
| Dollar_Cost_Points_Redeemed | int | Dollar value of redeemed points |

### 📐 Dimension Tables
| Table | Key Columns | Description |
|-------|------------|-------------|
| Dim_Customer | Id_Cus | Education, Salary, Marital Status, CLV |
| Dim_Date | DateKey | Year, Month, Quarter, MonthName |
| Dim_Geography | GeoID | Country, Province, City, PostalCode |
| Dim_LoyaltyCard | LoyaltyCardID | Card types: Aurora, Nova, Star |
| Dim_Enrollment | EnrollID | Standard, 2018 Promotion |
| Dim_Gender | ID_Gender | Male / Female |

---

## 🛠️ Tech Stack

| Tool | Purpose |
|------|---------|
| SQL Server | Database engine for ODS, STG & DWH |
| SSIS | ETL Pipeline (Extract, Transform, Load) |
| Power BI | Interactive dashboards & visualizations |
| T-SQL | Data transformations & stored procedures |
| Visual Studio | SSIS project development |

---

## 📊 Power BI Dashboard

The report contains **3 interactive pages** with slicers for Year, Month, Province, and Card Type.

### 1️⃣ Overview Page
![Overview](Airline-Loyalty-Analytics%20main/Screenshot%202026-06-15%20121300.png)

| KPI | Value |
|-----|-------|
| Total Customers | 17K |
| Total CLV | $133.71M |
| Total Distance | 762M km |
| Cancellation Rate | 12.35% |

**Visuals:** Avg CLV by Enrollment Type · Avg Distance per Flight by Card Tier · Total Points Redeemed by Card Type · Customers by Marital Status · Total Revenue by Month

---

### 2️⃣ Customers Page
![Customers](Airline-Loyalty-Analytics%20main/Screenshot%202026-06-15%20121348.png)

| KPI | Value |
|-----|-------|
| Avg Salary | $59K |
| Active Customers | 15K |
| Total Customers | 17K |
| Avg CLV | $7.99K |

**Visuals:** Customers by Province (Map) · Gender Distribution · Marital Status · Avg Salary by Card Type · Customers by Education

---

### 3️⃣ Flight Activity Page
![Flight Activity](Airline-Loyalty-Analytics%20main/Screenshot%202026-06-15%20121435.png)

| KPI | Value |
|-----|-------|
| Total Flights | 235K |
| Avg Flights per Customer | 14.02 |
| Total Distance | 762M km |
| Avg Flights per Year | 13.80K |

**Visuals:** Customers by Card Type · Avg Distance by Tier · Avg Flights by Province · Monthly Flight Trends · Total Distance over Time

---

## 📁 Project Structure

```
Customer-Loyalty-DWH/
│
├── Airline-Loyalty-Analytics/        # SSIS - DWH ETL packages
│   ├── DWH.dtsx                      # DWH package
│   ├── ODS.dtsx                      # ODS package
│   ├── STG.dtsx                      # STG package
│   └── Project.params
│
├── Airline-Loyalty-Analytics main/   # Source data & Screenshots
│   ├── Customer Loyalty History.csv  # Source data
│   ├── Customer Flight Activity.csv  # Source data
│   ├── Calendar.csv                  # Source data
│   └── Screenshot *.png              # Dashboard screenshots
│
├── Task.pbix                         # Power BI dashboard
├── ODS.png                           # ODS schema diagram
├── STG.png                           # STG schema diagram
├── DWH.png                           # DWH schema diagram
└── kero Task.sln                     # Visual Studio solution
```

---

## 🖼️ Database Schemas

### Operational Data Store (ODS)
![ODS Schema](ODS.png)

### Staging Layer (STG)
![STG Schema](STG.png)

### Data Warehouse (DWH)
![DWH Schema](DWH.png)

---

## 👤 Author

**Mohamed Abdelhakim**
Data Engineer | BI Developer
🔗 [GitHub](https://github.com/MohamedAbdelhakim1)

---

## 🎓 Course

This project was built as part of the **NTI Hireready Data Engineering & Analysis** program.

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

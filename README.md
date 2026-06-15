# ✈️ Customer Loyalty Data Warehouse

> A complete **End-to-End Data Warehouse** solution for an airline customer loyalty program, built as part of the **NTI Hireready Data Engineering & Analysis Course**.

---

## 📌 Project Overview

This project implements a full **ETL pipeline** and **dimensional data model** to analyze customer flight activity, loyalty points, and enrollment behavior. The solution covers everything from raw data ingestion to interactive Power BI dashboards.

---

## 🏗️ Architecture

The project follows a **3-Layer Architecture**:

```
Source Data (CSV Files)
        ↓
[ODS] Operational Data Store  →  Raw data loaded from source systems
        ↓
[STG] Staging Layer           →  Cleaned & standardized data
        ↓
[DWH] Data Warehouse          →  Star Schema ready for analytics
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
Dim_Date → Dim_Customer → Dim_Enrollment → Dim_Gender
       → Dim_Geography → Dim_LoyaltyCard → Fact_Table
```

---

## 🗂️ Data Model

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
| Table | Description |
|-------|-------------|
| Dim_Customer | Demographics: Education, Salary, Marital Status, CLV |
| Dim_Date | Year, Month, Quarter, MonthName |
| Dim_Geography | Country, Province, City, PostalCode |
| Dim_LoyaltyCard | Card types: Aurora, Nova, Star |
| Dim_Enrollment | Enrollment types: Standard, 2018 Promotion |
| Dim_Gender | Male / Female lookup |

---

## 🛠️ Tech Stack

| Tool | Purpose |
|------|---------|
| SQL Server | Database engine for all 3 layers |
| SSIS | ETL Pipeline (Extract, Transform, Load) |
| Power BI | Interactive dashboards & visualizations |
| T-SQL | Data transformations & stored procedures |
| Visual Studio | SSIS project development |

---

## 📊 Power BI Dashboards

The report has **3 pages**:

### 1️⃣ Overview Page
![Overview Dashboard](Screenshots/overview.png)

**KPIs:**
- 17K Total Customers
- $133.71M Total CLV
- 762M Total Distance (km)
- 12.35% Cancellation Rate

**Visuals:**
- Avg CLV by Enrollment Type (2018 Promotion vs Standard)
- Avg Distance per Flight by Card Tier (Aurora, Nova, Star)
- Total Points Redeemed by Card Type
- Customer distribution by Marital Status
- Total Revenue by Month

---

### 2️⃣ Customers Page
![Customers Dashboard](Screenshots/customers.png)

**KPIs:**
- $59K Avg Salary
- 15K Active Customers
- 17K Total Customers
- $7.99K Avg CLV

**Visuals:**
- Total Customers by Province (Map)
- Gender distribution (Male 49.75% / Female 50.25%)
- Marital Status breakdown
- Avg Salary by Card Type
- Total Customers by Education level

---

### 3️⃣ Flight Activity Page
![Flight Activity Dashboard](Screenshots/flight_activity.png)

**KPIs:**
- 235K Total Flights
- 14.02 Avg Flights per Customer
- 762M Total Distance (km)
- 13.80K Avg Flights per Year

**Visuals:**
- Customer count by Card Type (Star 45.39%, Nova 34.02%, Aurora 20.59%)
- Avg Distance per Flight by Tier
- Avg Flights by Province
- Avg Flights per Month trend
- Total Distance over time

---

## 📁 Project Structure

```
Customer-Loyalty-DWH/
│
├── kero Task/               # SSIS project - DWH ETL packages
│   ├── Dim_Date
│   ├── Dim_Customer
│   ├── Dim_Enrollment
│   ├── Dim_Gender
│   ├── Dim_Geography
│   ├── Dim_LoyaltyCard
│   └── Fact_Table
│
├── Task kero/               # SSIS project - ODS ETL packages
│   ├── Calendar
│   ├── Customer Flight Activity
│   └── Customer Loyalty History
│
├── Task.pbix                # Power BI dashboard (3 pages)
├── ODS.png                  # ODS layer schema
├── STG.png                  # Staging layer schema
├── DWH.png                  # Data Warehouse schema
└── kero Task.sln            # Visual Studio solution file
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

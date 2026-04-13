# 🍊 Swiggy Sales Analytics — Microsoft Fabric & Power BI

> **End-to-end data pipeline project** built using Microsoft Fabric, SQL, and Power BI.  
> Covers data ingestion, cleaning, star schema modelling, DAX measures, and an interactive dashboard.

---

## 📊 Key Metrics (Live from Semantic Model)

| Metric | Value |
|---|---|
| Total Orders | 197,430 |
| Total Revenue | ₹5.30 Crore |
| Average Order Value | ₹268.51 |
| Data Coverage | January – August |
| Restaurants Analysed | 50+ |
| Star Schema Tables | 5 (1 Fact + 4 Dimensions) |

---

## 🏗️ Architecture Overview

```
Raw CSVs
   └── Microsoft Fabric Lakehouse (Raw_Data/)
         └── SQL Cleaning & Validation (Fabric SQL Endpoint)
               └── Data Warehouse (Star Schema)
                     └── Power BI Semantic Model (DirectQuery)
                           └── Power BI Dashboard
```

### Star Schema

| Table | Type | Description |
|---|---|---|
| `fact_orders` | Fact | Order-level records: price, rating, rating_count |
| `dim_date` | Dimension | Date intelligence: Month, Quarter, Day with sort columns |
| `dim_restaurant` | Dimension | Restaurant name lookup |
| `dim_dish` | Dimension | Dish category, name, Food Type (calculated) |
| `dim_location` | Dimension | State, city, location hierarchy |

---

## 💡 Key Findings

1. **KFC vs McDonald's Revenue Divergence** — McDonald's leads on order volume (13,530) but KFC leads on revenue (₹42.5L) due to a ~32% higher average order value (₹327 vs ₹247). Revenue leadership ≠ volume leadership.

2. **Stable Demand Across 8 Months** — Monthly orders vary less than 9% (23K–25.4K range), suggesting strong baseline demand unaffected by seasonal patterns.

3. **QSR Chain Dominance** — Top 5 revenue restaurants are all QSR chains (KFC, McDonald's, Pizza Hut, Burger King, Domino's), representing significant platform GMV concentration.

4. **Rating Data Captured, Not Yet Activated** — `fact_orders` contains `rating` and `rating_count` for every order — an untapped analytical asset for quality monitoring and restaurant performance scoring.

---

## 📁 Repository Structure

```
swiggy-fabric-analytics/
│
├── README.md                          # This file
├── Swiggy_Sales_Dashboard.pbix        # Power BI Desktop file (model + visuals)
│
├── data/
│   └── raw/                           # Source CSV datasets
│       ├── customers.csv
│       ├── restaurants.csv
│       ├── orders.csv
│       ├── delivery_partners.csv
│       └── deliveries.csv
│
├── sql/
│   ├── 01_cleaning.sql                # Data validation & cleaning queries
│   ├── 02_warehouse_ddl.sql           # CREATE TABLE scripts (star schema)
│   └── 03_data_load.sql               # Lakehouse → Warehouse load scripts
│
├── screenshots/                       # Dashboard screenshots (captured during trial)
│   ├── dashboard_overview.png
│   ├── restaurant_performance.png
│   └── monthly_trend.png
│
└── docs/
    ├── Project_Report.docx            # Full technical & business report
    └── Business_Requirement.docx      # Original project brief
```

---

## ⚙️ Technology Stack

| Layer | Technology |
|---|---|
| Data Storage | Microsoft Fabric Lakehouse |
| Data Cleaning | Fabric SQL Analytics Endpoint |
| Data Warehousing | Fabric Data Warehouse |
| Orchestration | Fabric Data Pipelines |
| Semantic Layer | Power BI Semantic Model (DirectQuery) |
| Visualisation | Power BI Reports |

---

## ⚠️ Important Note — Trial Environment

This project was built on a **Microsoft Fabric free trial**, which means:

- The `Swiggy_Sales_Dashboard.pbix` file connects to `powerbi://api.powerbi.com/v1.0/myorg/Capstone` via DirectQuery
- **Visuals will render blank** without an active Fabric connection to the semantic model (`swiggy_semantic`)
- The **data model structure, relationships, DAX measures, and visual layout are fully intact** in the .pbix file
- All key metrics, table schemas, and insights are documented in the [`Project Report (DOCX)`](https://raw.githubusercontent.com/Xicor20/Swiggy-Analytics-with-Microsoft-Fabric/main/Swiggy_Analytics_Project_Report.docx)
- Dashboard screenshots taken during the live trial are in the [`screenshots/`](screenshots/) folder

This is a **known constraint of Fabric trial accounts** — the analytical design, modelling decisions, and DAX implementation are the primary portfolio artefacts.

---

## 📐 DAX Measures

```dax
-- Total Sales
Total Sales = SUM(fact_orders[price])

-- Total Orders  
Total Orders = COUNTROWS(fact_orders)

-- Average Order Value
Average Order Value = DIVIDE([Total Sales], [Total Orders])
```

All measures use ₹ (en-IN) currency format.

---

## 🚀 How to View This Project

1. **Read the report** → [`Project_Report.docx`](https://raw.githubusercontent.com/Xicor20/Swiggy-Analytics-with-Microsoft-Fabric/main/Swiggy_Analytics_Project_Report.docx)
 — complete documentation with live data metrics, schema, and insights
2. **View screenshots** → [`screenshots/`](screenshots/) — dashboard visuals from the live trial
3. **Inspect the model** → Open `Swiggy_Sales_Dashboard.pbix` in Power BI Desktop to see the star schema, relationships, and DAX measures (data will not load without Fabric connection)


---

## 🎯 Skills Demonstrated

- Microsoft Fabric end-to-end pipeline (Lakehouse → Warehouse → Semantic Model → Report)
- Star schema data modelling with surrogate keys
- SQL data cleaning and validation (referential integrity, deduplication, type correction)
- DirectQuery semantic model configuration
- DAX measure development with proper format strings
- Power BI report design and Fabric workspace publication

---

## 🤝 Connect  

- 📧 Email: tusharpokhariyal@gmail.com
- 🌐 LinkedIn: https://www.linkedin.com/in/tushar-pokhariyal/ 

---

*Built as a capstone project to learn Microsoft Fabric during free trial. January–August dataset. All data is synthetic/sample data for learning purposes.*

# Data Visualization for Business Optimization – MySQL + Power BI ETL Pipeline

## 📌 Problem Statement
Businesses often face supply chain inefficiencies due to scattered and unprocessed inventory data.  
In our case, product availability, demand, and pricing were stored in **separate datasets** across environments, making it difficult to:

- Identify supply shortages
- Track demand vs. availability trends
- Calculate profit/loss at a glance

This caused delayed decision-making and loss of potential revenue.  
The challenge was to **merge, clean, and visualize** large datasets in a way that provides **real-time actionable insights** for business optimization.

---

## 🎯 Solution Overview
I built an **ETL (Extract, Transform, Load) pipeline** using **MySQL** and **Power BI** that:

- **Extracts** inventory and product datasets from both test and production environments.
- **Transforms** the data by merging, cleaning, and standardizing it in MySQL.
- **Loads** the processed data into Power BI to create interactive dashboards for **supply chain monitoring**.

This ensures **data consistency**, **scalable reporting**, and **faster business decisions**.

---

## 🛠️ Tech Stack
- **Database:** MySQL
- **Visualization:** Power BI (Desktop & Service)
- **Query Language:** SQL (joins, updates, filtering, aggregation)
- **DAX:** Custom measures for KPIs
- **Environments:**
  - **Test Environment**
    - `products(1)`
    - `Test+environment+inventory+Dataset(1)`
  - **Production Environment**
    - `products+(1)`
    - `Prod+environment+inventory+Dataset`

---

## ⚙️ ETL Pipeline Workflow

### 1️⃣ Extract
- Imported datasets into MySQL **test** and **production** environments.

### 2️⃣ Transform
- Merged products and inventory datasets using **LEFT JOIN** on `Product ID`.
- Cleaned null or invalid `Order Date` entries.
- Updated incorrect Product ID mappings.
- Created a final clean table `new_table` ready for reporting.

### 3️⃣ Load
- Connected Power BI directly to **MySQL Production** environment.
- Imported `new_table` and created measures with **DAX** for:
  - Average Demand per Day
  - Average Availability per Day
  - Total Supply Shortage
  - Total Profit & Total Loss
  - Average Daily Loss

---

## 📊 Key Insights Delivered
- **Average Demand per Day:** 48.65
- **Average Availability per Day:** 24.70
- **Total Supply Shortage:** 61K units
- **Total Profit:** $301K
- **Total Loss:** $8M
- **Average Daily Loss:** $2.97K

---

## 📷 Dashboard Previews

### **Supply Chain Metrics**
![Supply Chain Metrics](images/supply_chain_metrics.png)

### **Profit & Loss Analysis**
![Profit & Loss Analysis](images/profit_loss_analysis.png)

---

## 🖼 Dashboard Snap (Full View)
> *Complete view of the Power BI dashboard combining KPIs, trends, and loss breakdown for supply chain monitoring.*

![Full Dashboard](images/full_dashboard.png)

---

## 🚀 How to Run Locally

### 1. Import Datasets into MySQL
- Create `test_env` and `prod` databases.
- Import provided CSV/XLSX datasets into respective environments.

### 2. Run SQL Scripts
```sql
-- Example: Merging datasets
CREATE TABLE new_table AS
SELECT a.`Order Date (DD/MM/YYYY)`, a.`Product ID`, a.`Availability`, a.`Demand`,
       b.`Product Name`, b.`Unit Price ($)`
FROM `prod+environment+inventory+dataset` AS a
LEFT JOIN `products+(1)` AS b
ON a.`Product ID` = b.`Product ID`;



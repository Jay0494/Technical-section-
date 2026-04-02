
# ⚙️ Real Estate Analytics – Technical Implementation

## 🧠 Architecture Overview

### 🔧 Tech Stack

* **Snowflake** → Cloud Data Warehouse
* **Power BI** → Data Modeling & Visualization
* **DAX** → Metric Engineering & Calculations
* **Power Query** → Data Transformation & Shaping

---

## 🔗 Live Dashboard & Assets

👉 **[🚀 View Interactive Dashboard](https://app.powerbi.com/view?r=eyJrIjoiMzE0YjVkZDktZjZjMC00Mjk0LWI2MTItOWU1MzdhYmYyNzAyIiwidCI6ImIyMTFiMjkwLWFkNzUtNGJlNC1iZDk3LWI5Y2MxZDlmMzdlZCJ9)**



---

## 🔄 Data Pipeline

1. Extracted structured data from **Snowflake warehouse**
2. Performed **data validation and transformation** in Power Query
3. Built an optimized **analytical model in Power BI**
4. Delivered **KPI-driven dashboards** for business decision-making

---

## 🏗️ Data Model (Galaxy Schema)

### 📊 Fact Tables

* `fact_inquiry_table`
* `fact_sales_table`
* `fact_rental_table`
* `fact_listing_history`

### 📁 Dimension Tables

* `dim_date`
* `dim_property`
* `dim_location`
* `dim_listing`
* `dim_event`

---

### 🧩 Design Approach

* Implemented a **Galaxy Schema** to support multi-domain analytics
* Enforced **one-to-many relationships** across all dimensions
* Enabled **centralized filtering** using conformed dimension tables

---

## ⚠️ Data Quality Issue & Resolution

### ❌ Problem

Unexpected **many-to-many relationship** in the model

### 🔍 Root Cause

Duplicate records in the **listing table**

### ✅ Solution

* Removed duplicates at source level
* Validated **primary key uniqueness**
* Re-established correct **one-to-many relationships**

👉 Result: Restored model integrity and eliminated ambiguous filtering

---

## 📊 Core DAX Measures

### 🔹 Base Measures

```DAX
Total Inquiries = COUNT(fact_inquiry_table[Inquiry_ID])

Total Leads = 
CALCULATE(
    COUNT(fact_inquiry_table[Inquiry_ID]),
    fact_inquiry_table[Is_Qualified] = TRUE()
)

Total Closed Deals = COUNT(fact_sales_table[Listing_ID])
```

---

### 🔹 Conversion Metrics

```DAX
Lead Conversion Rate % = 
DIVIDE([Total Leads], [Total Inquiries], 0)

Conversion Rate % = 
DIVIDE([Total Closed Deals], [Total Leads], 0)
```

---

### 🔹 Operational Metrics

```DAX
Avg Days on Market = 
AVERAGE(fact_sales_table[DAYS_ON_MARKET])

Avg Response Time = 
AVERAGE(fact_inquiry_table[Response_Time_Hours])
```

---

### 🔹 Time Intelligence

```DAX
Previous Year DOM = 
CALCULATE(
    [Avg Days on Market],
    SAMEPERIODLASTYEAR(dim_date[Date])
)

DOM YoY % = 
DIVIDE(
    [Avg Days on Market] - [Previous Year DOM],
    [Previous Year DOM],
    0
)
```

---

## 🧠 Modeling Strategy

### 1. Context Control

* Leveraged `CALCULATE()` for dynamic filter manipulation
* Used `ALL()` for normalization and ratio-based metrics

---

### 2. Measure Layering

* Structured measures as:
  **Base → Derived → KPI**

👉 Improves scalability, readability, and maintainability

---

### 3. Time Intelligence

* Implemented a **dedicated Date table**
* Standardized **YoY calculations** across KPIs

---

### 4. Performance Optimization

* Eliminated **many-to-many joins**
* Reduced model ambiguity
* Optimized aggregations for faster query performance

---

## 📷 Assets

### 📊 Data Model
<img width="1145" height="681" alt="model 349" src="https://github.com/user-attachments/assets/f22084b3-8c43-4d7b-842a-7292b10f316e" />

### 📈 Dashboard
<img width="1564" height="943" alt="dashboard project 349" src="https://github.com/user-attachments/assets/face625e-00ba-4d2c-8513-1b6fe77a70f0" />

---

## 🚀 Technical Outcome

* Built a **scalable and production-ready analytical model**
* Ensured **data integrity and relational accuracy**
* Delivered a **high-performance BI solution**
* Enabled **accurate, context-aware reporting across business layers**

---

## 🔥 Technical Philosophy

> **A dashboard is only as good as the model behind it.**

This project demonstrates:

* Strong **data modeling principles**
* Clean and scalable **DAX design**
* Business-aligned **metric engineering**

---

**[Click to go Back to Analysis page](https://github.com/Jay0494/real-estate-analysis.git)**

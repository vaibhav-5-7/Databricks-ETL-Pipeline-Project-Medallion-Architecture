Here is the **clean, final README — ONLY the text** so you can directly **copy & paste** into GitHub.

---

# **Databricks ETL Pipeline Project – FMCG Data**

This project demonstrates an end-to-end **ETL pipeline** built using **Databricks, PySpark, SQL, Delta Lake, and Medallion Architecture**.
The dataset represents a simplified **FMCG domain**, containing **Customers, Products, Orders, and Gross Price** data.

The objective is to design a scalable data engineering workflow using:

* Medallion Architecture (Bronze → Silver → Gold)
* PySpark transformations
* SQL modeling
* Delta Lake features (ACID, MERGE, Time Travel)
* Databricks Jobs for automated orchestration
* Fact & Dimension modeling (Star Schema)

---

## **Project Architecture**

```
RAW DATA (CSV)
     │
     ▼
BRONZE LAYER (Raw Ingestion)
- customers
- products
- orders
- gross_price
     │
     ▼
SILVER LAYER (Cleaned & Standardized)
- type casting
- removing duplicates
- date normalization
- schema standardization
     │
     ▼
GOLD LAYER (Analytics-Ready)
- dim_customers
- dim_products
- dim_gross_price (SCD2)
- dim_date
- fact_orders
```

---

## **Tech Stack**

* Databricks
* PySpark
* SQL
* Delta Lake
* Unity Catalog
* Medallion Architecture
* Databricks Jobs (Workflows)

---

## **Datasets Used (FMCG Domain)**

1. **Customers** – customer details, platform, market
2. **Products** – product information
3. **Orders** – daily order transactions
4. **Gross Price** – product pricing with effective dates

---

## **ETL Pipeline Overview**

### **1. Bronze Layer – Raw Ingestion**

* Load raw CSV files into Delta tables
* Keep schema and data as-is for traceability

### **2. Silver Layer – Standardization**

* Clean, type cast, rename columns
* Convert date formats
* Remove duplicates
* Prepare refined data for modeling

### **3. Gold Layer – Dimensional Modeling**

**Dimensions created:**

* `dim_customers` – customer surrogate keys
* `dim_products` – product surrogate keys
* `dim_gross_price` – SCD Type-2 pricing history
* `dim_date` – generated from order dates

**Fact Table:**

* `fact_orders` – contains foreign keys to all dimensions
* Built using incremental MERGE operations

---

## **Incremental Load Logic**

### **Fact Orders**

```sql
MERGE INTO gold.fact_orders tgt
USING silver.orders src
ON tgt.order_id = src.order_id
WHEN MATCHED THEN UPDATE SET *
WHEN NOT MATCHED THEN INSERT *
```

### **Dim Gross Price (SCD2)**

* Track price changes using `effective_from`, `effective_to`, and `is_current` flags
* New record created for every price update

---

## **Databricks Job Orchestration**

A 4-step automated workflow:

1. **Bronze Ingestion**
2. **Silver Transformation**
3. **Gold Dimension Build**
4. **Gold Fact Table Build**

Tasks run sequentially using Databricks Jobs.

---

## **Final Outputs**

* Clean and reliable Gold-layer dimension tables
* Fact table ready for analytics and reporting
* Automated ETL workflow with Delta Lake
* Fully implemented Medallion Architecture

---

## **Author**

**Vaibhav Panade**
Data Engineering | PySpark | Databricks | Delta Lake | ETL Pipelines

---

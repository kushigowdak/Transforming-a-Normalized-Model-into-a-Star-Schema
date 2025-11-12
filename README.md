# 🌟 Transforming a Normalized Model into a Star Schema
 

---

## 🎯 Project Overview
This project focuses on transforming a **normalized relational data model** into a **Star Schema** structure.  
The goal is to enhance query performance, simplify analytical queries, and organize data for efficient reporting and business intelligence.

Using **dbt (Data Build Tool)**, the project implements a layered architecture with staging (raw) and analytics (marts) models that reshape normalized data into well-defined **fact** and **dimension** tables.

---

## 🧩 Key Objectives
- Build a **Star Schema** data model optimized for analytics  
- Improve **query performance** and reporting speed  
- Simplify data retrieval and business analysis  
- Ensure data consistency across all entities  
- Separate **transactional (fact)** and **descriptive (dimension)** data layers  
- Provide a **scalable foundation** for data warehousing and BI tools  

---

## 🧠 Tools and Technologies
- **dbt (Data Build Tool)** – data transformation and modeling  
- **SQL** – query logic and transformation scripts  
- **Database** – Snowflake / BigQuery / Redshift / PostgreSQL  
- **IDE** – VS Code / dbt Cloud / SQL Workbench  
- **Data Source** – SALES_DB (sample normalized dataset)  
- **Visualization** – ER diagrams for schema design  

---

## 📁 Project Structure

```

models/
│
├── analytics/
│   ├── customer_dimension.sql
│   ├── employee_dimension.sql
│   ├── office_dimension.sql
│   ├── orders_fact.sql
│   └── product_dimension.sql
│
├── raw/
│   ├── raw_customers.sql
│   ├── raw_employees.sql
│   ├── raw_offices.sql
│   ├── raw_order_details.sql
│   ├── raw_orders.sql
│   ├── raw_product_lines.sql
│   ├── raw_products.sql
│   └── sources.yml
│
├── dbt_project.yml
├── packages.yml
└── README.md

````

---

## ⚙️ Project Workflow

### 1️⃣ Source Analysis
- Analyze the **normalized schema** and identify relationships between tables  
- Determine **primary** and **foreign keys** to support joins  

### 2️⃣ Data Modeling Setup
- Initialize a new **dbt project** and configure the connection profile  
- Organize models into two main layers:
  - `raw/` → staging and data cleaning  
  - `analytics/` → fact and dimension modeling  

### 3️⃣ Staging Models
- Develop SQL models under `raw/` to prepare and clean source data  
- Standardize column names, data types, and handle nulls  

### 4️⃣ Star Schema Design
- Define the **fact table** (`orders_fact`) and **dimension tables**:
  - `customer_dimension`
  - `product_dimension`
  - `employee_dimension`
  - `office_dimension`
- Create surrogate keys and establish relationships between fact and dimension tables  

### 5️⃣ Build Models
- Create transformation logic using **dbt models**:
  - **Dimension tables**: contain unique keys and descriptive attributes  
  - **Fact tables**: contain measurable data and foreign keys referencing dimensions  

### 6️⃣ Testing and Validation
- Run all models using:
  ```bash
  dbt run
````

* Validate results and relationships with SQL queries

### 7️⃣ Performance Review

* Test query performance between the normalized and star schema models
* Confirm that analytical queries execute faster on the star schema

---

## 🗺️ Star Schema Diagram

```
                +----------------------+
                |  CUSTOMER_DIMENSION  |
                +----------------------+
                          |
                          |
                +----------------------+
                |     ORDERS_FACT      |
                +----------------------+
                  /       |        \
                 /        |         \
+----------------+   +----------------+   +----------------+
| PRODUCT_DIMENSION | | EMPLOYEE_DIMENSION | | OFFICE_DIMENSION |
+----------------+   +----------------+   +----------------+
```

---

## 💡 Example Analytical Query

```sql
SELECT 
    c.customer_name,
    p.product_name,
    SUM(f.sales_amount) AS total_sales
FROM {{ ref('orders_fact') }} f
JOIN {{ ref('customer_dimension') }} c ON f.customer_key = c.customer_key
JOIN {{ ref('product_dimension') }} p ON f.product_key = p.product_key
GROUP BY c.customer_name, p.product_name
ORDER BY total_sales DESC
LIMIT 10;
```

---

## 🚀 Results

* Query performance improved significantly after transformation
* Simplified joins between tables for reporting and dashboarding
* Established a scalable architecture for future data models and metrics
* Enhanced compatibility with BI tools such as Tableau and Power BI

---


## 🏁 Conclusion

This project demonstrates the end-to-end process of converting a **normalized database** into a **Star Schema** using **dbt**.
The new schema provides:

* Faster analytics
* Cleaner data relationships
* Easier integration with data visualization tools
* A strong foundation for scalable, enterprise-level data warehousing


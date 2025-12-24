# Customer Orders ETL Pipeline – Quick Overview

## Objective
End-to-end ETL pipeline for **customer and order data** using **PySpark** and **Delta Lake** on Databricks.  
- Ingest raw data → Bronze  
- Apply **SCD Type-1** → Silver  
- Aggregate metrics → Gold  
- Support incremental daily updates  

---

## Architecture
**Bronze → Silver → Gold** (Medallion Architecture)

- **Bronze:** Raw data ingestion, append-only  
- **Silver:** Deduplication, SCD Type-1 merge  
- **Gold:** Customer-level aggregates & analytics  

---

## Data Flow
1. **Bronze:** Load CSVs into `bronze_db.customers` & `bronze_db.orders`  
2. **Silver:** Deduplicate by `ingestion_ts` and merge changes using Delta MERGE  
3. **Gold:** Join Silver tables on `customer_id`, compute metrics:  
   - total_orders, total_amount, avg_amount, max_order_amount, min_order_amount  
   - Keep latest customer attributes (name, email, city)  

---

## Key Features
- **SCD Type-1** in Silver for both customers and orders  
- Incremental load support  
- Idempotent and safe reruns  
- Job orchestration with **Databricks notebooks and tasks**  

---

## Tech Stack
- Databricks  
- PySpark  
- Delta Lake  
- GitHub  

---

## Interview Tip
> “This pipeline ingests raw customer and order data into Bronze, applies SCD Type-1 transformations in Silver, and builds customer-level aggregated analytics in Gold. Gold reflects latest attributes and metrics, supporting daily incremental updates in an idempotent and reliable manner.”


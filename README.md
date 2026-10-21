# Professional Data Analytics & Operational Governance Portfolio

Welcome to my technical analytics portfolio. As an analyst with a Master’s degree in Philosophy specializing in institutional governance and systemic ethics, paired with a professional background as a Marketing Specialist, I focus my data pipeline on data quality, data auditing, structural cleaning, and compliance verification.

Below are production-ready SQL and Python data-wrangling models designed to solve complex, real-world corporate operational challenges.

---

## Project 1: Multi-Channel Supply Chain & Logistics Revenue Leakage Audit
* **Case Study Framework:** This project is a simulated case study modeled after global industrial distribution frameworks. It demonstrates my ability to audit raw regional supplier datasets, calculate financial losses from late drop-offs, and track vendor reliability metrics.
* **The SQL Cleaning Solution:** This query filters for delayed shipments, aggregates the total number of delays per supplier, and calculates the total financial impact to protect factory assembly lines.

```sql
SELECT
  supplier_name,
  COUNT(shipment_id) AS total_late_shipments,
  SUM(shipping_cost) AS total_late_cost
FROM
  shipments
WHERE
  delivery_status = 'Late'
GROUP BY
  supplier_name
ORDER BY
  total_late_shipments DESC;
```

---

## Project 2: Automated Data Sanitisation & High-Risk Parameter Filtering
* **Case Study Framework:** This project is a data governance model built to mirror strict international regulatory standards. It showcases my ability to segment highly sensitive information and enforce strict quality guardrails across database rows.
* **The SQL Solution:** This query filters a sensitive operational database using multiple strict parameters to ensure specific high-risk cohorts are safely isolated for advanced statistical reporting.

```sql
SELECT
  patient_id, 
  age,
  dosage_mg
FROM
  clinical_trials
WHERE
  age > 55 
  AND blood_pressure_sys > 140;
```

---

## Project 3: E-Commerce Customer Engagement & Operational Metric Reconciliation
* **Case Study Framework:** Inspired by my professional background as a Marketing Specialist managing campaign performance data and customer feedback loops, I designed this data preparation pipeline. It simulates a fast-growing digital platform to demonstrate text standardization, string normalization, and identifying revenue leakage from operational bottlenecks.
* **The SQL Solution:** This query executes heavy string normalization (`TRIM` and `UPPER`) to group duplicate data entries caused by manual restaurant inputs, and uses conditional logic (`SUM(CASE WHEN)`) to isolate financial loss tied to severe delivery delays.

```sql
SELECT 
  UPPER(TRIM(restaurant_name)) AS cleaned_restaurant_name,
  COUNT(order_id) AS total_orders,
  SUM(CASE WHEN delivery_time_minutes > 45 THEN order_value_sek ELSE 0 END) AS total_delayed_revenue_loss
FROM 
  raw_delivery_logs
WHERE 
  order_value_sek > 0 
  AND client_id IS NOT NULL
GROUP BY 
  UPPER(TRIM(restaurant_name))
ORDER BY 
  total_delayed_revenue_loss DESC;
```

---

## Programmatic Pre-Cleaning Audit (Python & Pandas)
* **Operational Intent:** Before injecting raw, decentralized logistics spreadsheets into a production database, I run programmatic structural checks to audit file schemas, map null constraints, and verify type limits.

```python
import pandas as pd

# Load raw operational CSV tracking data
df = pd.read_csv("hotmat_raw_orders.csv")

# 1. Structural audit: verify memory footprint and data schemas
print("--- Structural Data Schema ---")
print(df.info())

# 2. Inspect record footprints for syntax padding or alignment anomalies
print("\n--- Top 5 Sample Records ---")
print(df.head())

# 3. Calculate absolute volume of missing/null data fields per column
print("\n--- Missing Field Matrix ---")
print(df.isnull().sum())
```

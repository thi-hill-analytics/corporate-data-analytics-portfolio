# Professional Data Analytics & Governance Portfolio

Welcome to my technical portfolio. As an analyst with a Master’s degree in Philosophy, I focus my technical pipeline on data quality, data auditing, structural cleaning, and compliance verification.

Below are production-ready SQL and Python data-wrangling models designed for specific corporate operational scenarios.

---

## Project 1: Logistics Supply Chain Optimization
* **Business Problem:** Identifying unreliable shipping partners causing factory assembly line delays for Automobile Group Logistics.
* **The SQL Cleaning Solution:** This query filters for delayed shipments, aggregates the total number of delays per supplier, and calculates the total financial impact.

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

## Project 2: Clinical Trial Safety Filtering
* **Business Problem:** Extracting baseline safety data for high-risk patients (over 55 with high systolic blood pressure) before running biostatistical analysis.
* **The SQL Solution:** This query filters the clinical database using multiple parameters to ensure patient safety metrics are isolated.

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

## Project 3: Food.com Logistics & Order Data Reconciliation
* **Business Problem:** Standardizing inconsistent text inputs, handling missing drop-off metrics, and filtering programmatic system errors from raw food delivery logistics tracking streams.
* **The SQL Solution:** This query handles string normalization to group duplicate parameters and calculates revenue loss from extreme delivery delays.

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

## Programmatic Pre-Cleaning Audit (Python & Pandas)
Before injecting the raw logistics files into the database, I run programmatic structural checks to audit file schemas, map null constraints, and check type limits.

```python
import pandas as pd

# Load raw logistics CSV
df = pd.read_csv("hotmat_raw_orders.csv")

# 1. Structural audit: verify memory footprint and data schemas
print(df.info())

# 2. Inspect record footprints for padding anomalies
print(df.head())

# 3. Calculate absolute volume of missing data fields
print(df.isnull().sum())
```

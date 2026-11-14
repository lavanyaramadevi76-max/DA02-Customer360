# DA-02: Customer 360 and Marketing Attribution Platform

**Project:** Nexvia DA-02  
**Technologies:** Google BigQuery, SQL, dbt, Tableau, Python  
**Data source:** Google Analytics 4 (GA4) public obfuscated ecommerce sample dataset

## 1. Project Overview

This project develops a Customer 360 analytics prototype using GA4 ecommerce data in BigQuery, supplemented with synthetic CRM-style customer profiles and synthetic advertising spend data.

The objective is to analyze customer behavior, purchasing patterns, customer segments, historical customer lifetime value, and acquisition-channel performance through data transformations and interactive Tableau dashboards.

## 2. Technologies Used

- Google BigQuery – data storage and SQL transformations
- SQL – data preparation, cleaning, and analytical queries
- dbt Core with BigQuery adapter – modular data transformations and testing
- Tableau – dashboard development and visualization
- Python – CSV data validation
- Git and GitHub – version control and project documentation

## 3. Data Processing and Architecture

1. GA4 ecommerce sample data is stored in BigQuery.
2. SQL transformations prepare session and order datasets.
3. Synthetic CRM-style customer profiles and a deterministic pseudonymous identity map are used to construct the Customer 360 dataset.
4. RFM segmentation and historical CLV calculations are performed.
5. Acquisition-channel attribution is analyzed using available first-user acquisition fields.
6. Synthetic advertising spend is used for campaign analysis.
7. Processed datasets are exported for Tableau dashboards and Python validation.

## 4. dbt Implementation

The dbt project connects to the existing BigQuery `customer360` dataset.

**Models implemented:**

| Model | Materialization |
|---|---|
| stg_sessions | View |
| stg_orders | View |
| customer_360_dbt | Table |

**Completed dbt activities:**

- dbt connection and configuration
- Source definitions
- Staging and mart models
- Model documentation
- Three data tests successfully passed
- dbt run completed successfully
- dbt documentation generated and served

Verified output row counts:

| Model | Rows |
|---|---:|
| stg_sessions | 360,129 |
| stg_orders | 4,466 |
| customer_360_dbt | 270,154 |

The Customer 360 dbt model references the existing BigQuery Customer 360 table; it does not independently rebuild identity resolution.

## 5. Key Analytical Results

- Sessions: 360,129
- Unique users: 270,154
- Page views: 1,350,428
- Cleaned order records: 4,466
- Distinct order IDs: 4,451
- Purchasing customers in the Customer 360 dataset: 4,400
- Historical average CLV: approximately $82.01

### RFM Customer Segmentation

| Segment | Customers |
|---|---:|
| No Purchase | 265,754 |
| Recent Customers | 2,717 |
| Needs Attention | 1,535 |
| Loyal Customers | 114 |
| Champions | 34 |

## 6. Tableau Dashboard

The packaged Tableau workbook is `DA02_Customer360_Final.twbx`.

Dashboard analysis includes:

- Monthly Revenue Trend
- Monthly Orders
- Customer Segmentation
- Customer Lifetime Value
- Marketing Channel Performance

## 7. Important Project Limitations

- CRM-style customer profiles and advertising spend data are synthetic.
- Identity mapping is deterministic for available GA4 pseudonymous user IDs; it is not verified cross-device identity resolution.
- Attribution uses first-user acquisition source information as a proxy, not complete session-level customer journeys.
- Synthetic campaign names do not exactly match GA4 campaign names. Therefore, reliable campaign ROI and CPA cannot be calculated.
- CLV is historical, not predictive. Annualized estimates may be distorted by the short observation period.
- The dbt models reference existing BigQuery outputs and do not represent a fully rebuilt production pipeline.
- This project does not demonstrate a live Segment integration or production CRM integration.

## 8. Repository Contents

- `models/` – dbt staging and mart models, source definitions, and schema tests
- `dbt_project.yml` – dbt project configuration
- `profiles.yml.example` – example dbt connection configuration
- `DA02_Customer360_Final.twbx` – Tableau packaged workbook
- `DA02_Customer360_Project_Documentation.pdf` – project documentation
- CSV files – exported analytical datasets
- `validate_customer360.py` – Python validation script

## 9. Reproducibility

To execute the dbt project:

1. Install dbt Core and the BigQuery adapter.
2. Configure the local dbt profile using `profiles.yml.example`.
3. Authenticate with Google Cloud.
4. Run `dbt debug`.
5. Run `dbt run`.
6. Run `dbt test`.
7. Generate documentation using `dbt docs generate`.

Never upload local credentials, access tokens, or service-account JSON files to GitHub.

## 10. Conclusion

The DA-02 project demonstrates an analytical Customer 360 workflow using BigQuery, SQL, dbt, Tableau, and Python. It brings together customer, order, session, segmentation, historical CLV, and acquisition-channel analysis in a documented prototype while clearly identifying its data and methodology limitations.

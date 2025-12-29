# fabric-banking-de-project
end to end data engineering project on banking using microsoft fabric
Banking Data Engineering Pipeline – Microsoft Fabric
📌 Project Summary

This project demonstrates an end-to-end batch data engineering pipeline built on Microsoft Fabric Lakehouse, designed to reflect enterprise banking data platforms used in firms like JP Morgan / Morgan Stanley.

The solution ingests transactional and customer data, applies SCD Type 2, enriches facts, enforces data quality & audit controls, and exposes analytics-ready Gold tables for Power BI consumption.

🎯 Business Problem

Banks need:

Accurate transaction reporting

Historical customer attribute tracking

Trusted, auditable data pipelines

Scalable analytics-ready datasets

This project solves these using modern Lakehouse architecture.

🧱 Architecture (High Level)
Source
 → Bronze (Raw)
 → Silver (Cleaned)
 → SCD Customer Dimension
 → Enrichment
 → Gold Facts & Dimensions
 → Data Quality & Audit
 → Power BI Consumption

🛠️ Technology Stack

Cloud: Microsoft Fabric

Storage: OneLake (Delta Lake)

Compute: Spark (PySpark)

Orchestration: Fabric Pipelines

Analytics: Power BI (Direct Lake)

📂 Data Modeling (Star Schema)
Fact Table

gold_fact_transactions

txn_id

txn_date

customer_sk

merchant_sk

category_sk

amount

risk indicators

(Incremental / append-only)

Dimension Tables

gold_dim_customer (SCD Type 2)

gold_dim_merchant

gold_dim_category

(Surrogate keys, descriptive attributes)

🔁 SCD Type 2 – Customer Dimension

Tracks historical customer changes

Uses:

effective_start_date

effective_end_date

is_current flag

Enables point-in-time accurate reporting

🔍 Data Quality & Audit (Bank-Grade)

Implemented post-Gold validation:

Row count reconciliation (Silver → Gold)

Amount reconciliation

Critical null checks

Duplicate detection

Audit metadata stored in:

pipeline_audit_log (run status, counts, totals)

Ensures trust, traceability, and regulatory readiness.

⚙️ Orchestration (Fabric Pipelines)

Pipelines orchestrate Spark notebooks with:

Dependency-based execution

Daily batch scheduling

Automatic failure propagation

Safe reruns (idempotent design)

Pipeline flow:

Bronze → Silver → SCD → Enrich → Gold → DQ → Aggregates

🚀 Performance & Optimization

Fact tables partitioned by transaction date

Periodic OPTIMIZE + Z-ORDER on surrogate keys

VACUUM for storage cleanup

Aggregation tables for BI performance

📊 Consumption (Power BI)

Gold tables exposed via Direct Lake

Star-schema semantic model

Analysts build measures (DAX)

Engineers focus on data correctness & structure

🔑 Key Banking Concepts Demonstrated

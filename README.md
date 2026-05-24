# mobility-analysis-project

# 🚦 Mobility Analysis Project

A real-time mobility and traffic analytics pipeline built using Kafka, PySpark, Delta Lake, Hive Metastore, and Power BI following the Medallion Architecture (Bronze → Silver → Gold).

---

# 📌 Project Overview

This project simulates real-time mobility/traffic data ingestion, processing, transformation, and analytics using modern Data Engineering tools.

The pipeline performs:

- Real-time streaming ingestion using Kafka
- Data processing with PySpark Structured Streaming
- Delta Lake storage for ACID transactions
- Hive Metastore integration for table management
- Medallion Architecture implementation
- Dashboard visualization using Power BI

---

# 🏗️ Architecture

```text
Data Generator
      ↓
Kafka Producer
      ↓
Kafka Topic
      ↓
PySpark Streaming
      ↓
Bronze Layer (Raw Data)
      ↓
Silver Layer (Cleaned Data)
      ↓
Gold Layer (Business Metrics)
      ↓
Hive Metastore
      ↓
Power BI Dashboard



mobility-analysis/
│
├── apps/
│   ├── traffic_producer.py
│   ├── traffic_bronze.py
│   ├── traffic_silver.py
│   └── traffic_gold.py
│
├── hive-conf/
│   └── hive-site.xml
│
├── warehouse/
│   ├── traffic_bronze/
│   ├── traffic_silver/
│   └── fact_traffic/
│
├── docker-compose.yml
│
└── README.md
⚙️ Components Explanation
1. Kafka Producer

Generates fake mobility/traffic data using Faker library and pushes records into Kafka topics.

Example fields:

vehicle_id
speed
location
timestamp
congestion_level
2. Kafka Broker

Kafka acts as a distributed messaging system.

Responsibilities:

Receives streaming events
Stores events in topics
Serves data to Spark consumers
Ports
Port	Purpose
9092	Internal Docker communication
29092	External access from host machine
3. Bronze Layer

Stores raw streaming data exactly as received from Kafka.

Characteristics:

Append-only
No transformations
Historical raw storage

Storage Format:

Delta Lake
4. Silver Layer

Performs:

Data cleaning
Null handling
Schema enforcement
Flattening nested JSON
Type casting

Purpose:
Creates analytics-ready structured data.

5. Gold Layer

Contains business-level aggregated metrics.

Example:

Average traffic speed
Congestion trends
Area-wise vehicle count
Peak traffic hours

Used directly by:

Power BI
Reporting tools
Analysts
🥇 Medallion Architecture
Bronze Layer

Raw ingestion layer.

Silver Layer

Cleaned and transformed layer.

Gold Layer

Business analytics layer.

Benefits:

Scalability
Data quality
Easier debugging
Better governance
💾 Delta Lake

Delta Lake provides:

ACID Transactions
Schema Enforcement
Time Travel
Data Versioning
Streaming + Batch support

Used for reliable data lake storage.

🗃️ Hive Metastore

Hive Metastore stores metadata about:

Databases
Tables
Schema
Table locations

PostgreSQL is used as backend storage for Hive metadata.

🐳 Docker Containers

The project uses Docker Compose for orchestration.

Containers:

Kafka
Spark Master
Spark Worker
Hive Metastore
PostgreSQL
Kafka UI

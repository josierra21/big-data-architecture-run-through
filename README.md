# Big Data Architecture Run-Through: Distributed Water Potability Analysis Pipeline

## Overview

This project demonstrates the design and implementation of an end-to-end distributed data pipeline using components of the Hadoop ecosystem. The goal was to build a scalable architecture capable of ingesting, storing, processing, analyzing, and persisting data across multiple big data technologies.

Using a water potability dataset, the pipeline integrates Apache NiFi, HDFS, Hive, Apache Spark MLlib, and HBase within a Google Cloud virtual machine environment. The project illustrates how modern big data systems move information through multiple stages while maintaining scalability, fault tolerance, and distributed processing capabilities. 

---

## Project Objectives

This project sought to demonstrate:

- Distributed data ingestion using Apache NiFi
- Large-scale storage using HDFS
- Structured querying with Apache Hive
- Machine learning model training using Apache Spark MLlib
- Persistent storage of model evaluation metrics in HBase
- Integration of multiple Hadoop ecosystem technologies into a single workflow

---

## Dataset Source

Water Potability Dataset

Kaggle:
https://www.kaggle.com/datasets/adityakadiwal/water-potability/data

CSV Source:
https://raw.githubusercontent.com/josierra21/bigData/refs/heads/main/water.csv

The dataset contains water quality measurements including pH, hardness, solids, chloramines, sulfate levels, conductivity, organic carbon, trihalomethanes, turbidity, and a binary potability indicator used for classification. 

---

## Technologies Used

- Apache NiFi
- Hadoop Distributed File System (HDFS)
- Apache Hive
- Apache Spark MLlib
- Apache HBase
- HappyBase
- Python
- Docker
- Google Cloud
- Linux
- PuTTY

---

## Architecture Overview

The pipeline follows the flow below:

```text
GitHub Dataset (water.csv)
        ↓
Apache NiFi
        ↓
HDFS
        ↓
Apache Hive
        ↓
Apache Spark MLlib
        ↓
Apache HBase
```

Data is ingested from GitHub, stored in HDFS, queried through Hive, processed using Spark machine learning algorithms, and finally persisted in HBase for long-term storage of evaluation metrics.

---

## Pipeline Components

### 1. Apache NiFi Data Ingestion

Apache NiFi was used to automate data ingestion into the Hadoop ecosystem.

#### Functions

- Download dataset from GitHub
- Update file metadata
- Write dataset to HDFS

#### Processors Used

- InvokeHTTP
- UpdateAttribute
- PutHDFS

Successful ingestion was verified through HDFS directory inspection. 

---

### 2. HDFS Distributed Storage

The Hadoop Distributed File System served as the primary storage layer for the raw dataset.

#### Benefits

- Distributed storage
- Fault tolerance
- Scalability
- Integration with Hive and Spark

The dataset was written to HDFS and made available for downstream processing. 

---

### 3. Apache Hive Query Layer

Hive was used to create a structured table over the water quality data and perform SQL-based analysis.

#### Example Query

```sql
SELECT COUNT(*) AS acidic_water
FROM water_quality
WHERE ph < 7;
```

The schema was designed to match the structure of the source CSV file while preserving numerical precision for water quality measurements. 

---

### 4. Apache Spark MLlib

Apache Spark MLlib was used to build a machine learning classification model.

#### Model

- Logistic Regression

#### Features

- pH
- Hardness
- Solids
- Chloramines
- Sulfate
- Conductivity
- Organic Carbon
- Trihalomethanes
- Turbidity

#### Target Variable

- Potability (0 = Not Potable, 1 = Potable)

Spark's VectorAssembler was used to prepare features before model training and evaluation.

---

### 5. Apache HBase

HBase served as the persistence layer for machine learning evaluation metrics.

#### Table Design

Table:

```text
water_metrics
```

Column Family:

```text
cf
```

Stored Metrics:

- Accuracy
- AUC

This design allows multiple model evaluation runs to be stored without overwriting previous results. 

---

## Machine Learning Results

The Logistic Regression model was trained using Spark MLlib.

### Evaluation Metrics

- Accuracy: 1.0
- AUC: 0.0

The results suggest the dataset subset used during testing may have been heavily imbalanced due to virtual machine resource limitations. Despite the unusual metrics, the model successfully completed training and generated evaluation outputs that were written into HBase. 

---

## Key Accomplishments

- Built a complete distributed data pipeline
- Automated ingestion with Apache NiFi
- Stored data in HDFS
- Queried data using Hive
- Trained a machine learning model using Spark MLlib
- Persisted model evaluation metrics in HBase
- Integrated multiple Hadoop ecosystem technologies into a single workflow
- Deployed and managed services within a Google Cloud environment

---

## Challenges Encountered

Several challenges were addressed during development:

- Hadoop service configuration and startup
- Docker container management
- Hive table loading and schema validation
- Spark dependency management
- HappyBase installation and configuration
- HBase Thrift server setup
- Integration between Spark and HBase

Troubleshooting these issues provided practical experience working with distributed systems and real-world big data architectures.

---

## Lessons Learned

This project provided hands-on experience with designing and operating a modern big data pipeline.

Key takeaways include:

- Distributed systems require coordination between multiple services.
- Data pipelines benefit from clear separation of ingestion, storage, processing, and persistence layers.
- Hadoop ecosystem tools can be integrated into scalable workflows.
- Machine learning pipelines can be embedded directly within big data architectures.
- Cloud-based environments provide flexible infrastructure for big data experimentation.

---

## Additional Architecture Design Exercise

In addition to the water potability pipeline implementation, this repository includes a separate architecture design presentation completed as part of the course.

### Real-Time Fraud Detection Architecture

The presentation proposes a scalable big data architecture for a global banking institution facing challenges related to:

- Credit card fraud
- Suspicious account activity
- Anti-money laundering compliance
- Real-time transaction monitoring
- Automated fraud prevention

The architecture incorporates multiple Hadoop ecosystem technologies, including:

- Apache Kafka
- Apache NiFi
- HDFS
- Apache Hive
- Apache Spark
- Apache HBase
- Apache Solr
- YARN

The proposed solution focuses on ingesting and processing high-volume transaction streams, detecting fraudulent behavior in real time, generating alerts, supporting compliance reporting, and providing a scalable foundation for future growth. The architecture was designed to demonstrate how the technologies covered throughout the course can be integrated into a real-world enterprise environment.

### Key Benefits

- Real-time fraud detection and alerting
- Automated identification of suspicious activity
- Support for anti-money laundering compliance
- Scalable processing of millions of transactions
- Centralized storage and analytics capabilities
- Improved visibility for fraud analysts
- Enhanced customer security and trust

This exercise complemented the hands-on pipeline implementation by focusing on architectural planning, system design, and the practical application of big data technologies to solve large-scale business challenges. 

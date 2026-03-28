---
title: "Data Lake"
description: "What a data lake is, how it stores raw data at scale, and when to use a data lake versus a data warehouse."
date: 2026-03-28
categories: [Glossary]
tags: [data-lake, S3, analytics, data-engineering, storage]
related:
  - glossary/data-warehouse
  - glossary/lakehouse
  - glossary/etl
  - glossary/data-mesh
---

A data lake is a centralized repository that stores raw data in its native format at any scale - structured (CSV, Parquet), semi-structured (JSON, logs), and unstructured (images, documents, audio). Unlike a data warehouse, data is stored without pre-defining a schema, enabling flexibility in how the data is later queried and analyzed.

## How It Works

Data is ingested into the lake in its original format (schema-on-read) rather than being transformed to fit a predefined schema (schema-on-write). Consumers apply their own schema when reading data, depending on their specific analytical needs. This means the same raw data can serve multiple use cases without reprocessing.

On AWS, S3 is the standard data lake storage layer. AWS Lake Formation provides governance, access control, and cataloging. AWS Glue discovers schema and catalogs data. Athena enables SQL queries directly on S3 data without loading it into a database.

## Why It Matters for AI

AI and ML workloads need diverse data: training data in various formats, features extracted from multiple sources, model artifacts, inference logs. A data lake provides a single repository where data engineers, data scientists, and ML engineers can access the data they need without waiting for ETL pipelines to transform it into a warehouse schema.

Raw data preservation is particularly valuable because you cannot predict future analytical needs. Data that seems irrelevant today may become a critical training signal for a model developed next year.

## Data Lake vs. Data Warehouse

Data lakes store raw, multi-format data with schema-on-read. They excel at flexibility and AI/ML workloads. Data warehouses store structured, pre-processed data with enforced schemas. They excel at fast, repeatable business intelligence queries. Most organizations need both, which has led to the lakehouse architecture that combines their strengths.

## Practical Guidance

Use S3 with intelligent tiering for cost-effective storage. Implement data cataloging (AWS Glue Data Catalog) from the start - a data lake without a catalog becomes a "data swamp" where nobody can find anything. Enforce access controls via Lake Formation. Partition data by date and key dimensions to enable efficient querying. Use columnar formats (Parquet, ORC) for structured data to reduce query costs and improve performance.

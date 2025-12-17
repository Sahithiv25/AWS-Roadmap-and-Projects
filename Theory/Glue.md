## AWS Glue
AWS Glue is a fully managed, serverless ETL service used to discover, catalog, transform, and prepare data for analytics and machine learning.

#### Glue Data Catalog
A central metadata repository that stores: table schemas, column types, data locations (S3 paths) and partition information.
It doesnot store data it stores ONLY metadata.

"The Glue Data Catalog acts as a centralized metastore for datasets stored in S3, enabling services like Athena and Redshift Spectrum to query data using SQL."

#### Glue Crawlers (Schema Discovery)
Crawlers scan data in S3 (CSV,JSON etc), infer schema automatically, create or update tables in the glue data catalog.
When to use them:
- when raw data arrives in S3
- when schema may change
- before querying with Athena

Glue Crawlers automatically discover schemas from S3 data and populate the Glue Data Catalog, removing the need for manual table definitions.

#### Glue Jobs (ETL Execution)
Glue Job: A serverless spark job that performs ETL.
Glue jobs can:
- Read from S3, JDBC, dynamoDB
- transform data that is clean, join, filter
- write back to S3 or data warehouse
- use Pyspark or scala
Glue job types:
Spark (ETL) - use when large data processing
Python shell- use for lightweight scripts
streaming - for real-time data

#### Glue DynamicFrames vs DataFrames
DynamicFrames are schema-flexible and easier for evolving data, while Spark DataFrames are faster and better for structured data.
DynamicFrame:
- glue-native abstraction
- schema flexible
- handles semi-structured data better
DataFrame
- spark native
- faster
- requires schema consistency

#### The pipeline
Raw data -> S3 -> Glue Crawler -> Glue data catalog -> Athena SQL queries

Ingest raw data into S3, use Glue Crawlers to catalog it, and query it using Athena without provisioning servers.

#### Glue with ML pipelines
Glue is often used for ML training:
Worflow:
Raw data (S3) -> Glue Job (clean,normalize) -> Processed data (in S3) -> Sagemaker training.

#### Glue Partitions
Partitions are logical divisions of data (ex: by date, or region).
Ex: s3://bucket/events/year=2026/month=1/
Used for better performance and low cost.

#### Glue Security
Glue users IAM roles to read/write S3, write logs to cloudwatch.

#### Questions
Q1: What problem does Glue solve?
It automates schema discovery and serverless ETL for analytics and ML workloads.

Q2: Glue vs Lambda for ETL?
Lambda is good for lightweight transformations. Glue is better for large-scale batch ETL using Spark.

Q3: Glue vs EMR?
Glue is serverless and managed. EMR provides more control but requires cluster management.

Q4: Does Glue store data?
No. Glue stores metadata. The actual data remains in S3.

Q5: Glue vs Athena?
Glue catalogs and transforms data. Athena queries data using SQL.
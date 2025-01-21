# Building a Spotify Data Pipeline: An End-to-End Data Engineering Project with AWS

## About
This project demonstrates a complete data engineering pipeline built around Spotify data, utilizing various AWS services for data ingestion, processing, transformation, and storage. The aim is to provide a scalable, efficient, and automated solution for extracting, transforming, and loading (ETL) data to generate actionable insights.
## Workflow
This project implements an end-to-end data pipeline using AWS services for extracting, processing, storing, and querying Spotify data. Below is the detailed workflow for the project.
### 1. Data Extraction
#### Description:
A Lambda function is triggered every hour using Amazon CloudWatch.
This Lambda function extracts data from the Spotify API and saves it as raw JSON files.
#### Steps:
Use Spotify API to fetch data for songs, albums, and artists.
Store the extracted data in the raw_data/toprocessed/ folder in Amazon S3.

### 2. Data Processing and Transformation
#### Description:
When raw data is added to the toprocessed folder, an S3 event trigger invokes a Lambda function to process and transform the data.
#### Steps:
##### 1. Trigger Event:
S3 detects new files in the toprocessed folder.
The event invokes a transformation Lambda function.
##### 2. Processing and Transformation:
The raw JSON data is processed and structured into three categories:
Songs Data, Albums Data, Artists Data
##### 3. Store Transformed Data:
Save the transformed data in corresponding folders under transformed_data/:
transformed_data/songs_data/
transformed_data/albums_data/
transformed_data/artists_data/
##### 4. Cleanup:
Move the processed raw files from raw_data/toprocessed/ to raw_data/processed/.
Automatically delete files from raw_data/toprocessed/ to keep it clean.
### 3. Data Cataloging
#### Description:
AWS Glue Crawlers are used to crawl the transformed data folders and create/update a schema in the Glue Data Catalog.
#### Steps:
##### 1. Crawler Configuration:
Configure Glue Crawlers to crawl the folders:
transformed_data/songs_data/
transformed_data/albums_data/
transformed_data/artists_data/
##### 2. Schema Creation:
Crawlers extract metadata from the transformed files and generate schemas for songs, albums, and artists.
The schema is stored in the AWS Glue Data Catalog.
### 4. Querying and Analytics
#### Description:
AWS Athena is used for querying the transformed data using SQL.
#### Steps:
##### 1. Data Source Setup:
Set up an Athena query environment to connect to the Glue Data Catalog.
##### 2. SQL Queries:
Write and execute SQL queries to analyze the songs, albums, and artists datasets.
Example Queries:
Most popular songs based on Spotify's popularity metric.
Albums with the highest number of tracks.
Artist collaborations across different songs.

## Technologies and Tools Used
### Programming Language: 
Python (with Boto3 for AWS SDK)
### Services:
1. Spotify API: For extracting data.
2. Amazon S3: For storing raw and transformed data.
3. AWS Lambda: For data extraction and transformation.
4. Amazon CloudWatch: For scheduling the extraction Lambda function.
5. AWS Glue: For creating and managing a data catalog.
6. AWS Athena: For SQL-based querying of the transformed data.






   
  

# Stock Market Kafka Real-Time Data Engineering Project

## 📌 Introduction
This project demonstrates an **end-to-end real-time data engineering pipeline** for stock market data using **Apache Kafka** and **AWS services**.  
We built a system that ingests live stock data with Python, streams it through Kafka running on EC2, stores it in Amazon S3, and makes it queryable with AWS Glue and Athena.

## 🏗️ Architecture
**Producer → Kafka Broker (EC2) → Consumer → Amazon S3 → Glue Crawler → Glue Catalog → Athena**

1. **Producer (Python + yFinance)**: Collects live stock data and publishes to a Kafka topic.  
2. **Kafka Broker (EC2)**: Streams the data in real-time.  
3. **Consumer (Python)**: Reads messages from Kafka and writes gzipped JSON files into S3.  
4. **AWS Glue Crawler & Catalog**: Creates schema definitions from S3 data.  
5. **AWS Athena**: Queries real-time data directly from S3.

## 🛠️ Technologies Used
- **Programming Language**: Python  
- **AWS Services**:  
  - Amazon S3 (data lake storage)  
  - Glue Crawler & Glue Catalog (schema & metadata)  
  - Athena (interactive SQL queries)  
  - EC2 (Kafka cluster host)  
- **Apache Kafka**: Event streaming platform for real-time data ingestion  
- **SQL**: Data querying & analysis  

## 📂 Dataset
We focused on the **data pipeline & operations**, so any stock dataset can be used.  
Dataset used in the original reference project:  
👉 [indexProcessed.csv](https://github.com/darshilparmar/stock-market-kafka-data-engineering-project/blob/main/indexProcessed.csv)


## 🚀 How to Run
1. Launch an **EC2 instance (Amazon Linux 2, free-tier eligible)**.  
2. Install **Java** and **Kafka 3.3.1**.  
3. Configure `server.properties` with both local and public listeners.  
4. Start **ZooKeeper** and **Kafka broker**.  
5. Create Kafka topic `stocks_raw`.  
6. Run the **producer** to publish stock prices.  
7. Run the **consumer** to store messages in S3.  
8. Create a **Glue Crawler** → generate schema in Glue Catalog.  
9. Query the ingested data using **Athena**.

## 📊 Example Athena Query
```sql
SELECT symbol, AVG(last_price) AS avg_price
FROM stocks_raw
WHERE ingestion_date = '2025-08-26'
GROUP BY symbol
ORDER BY avg_price DESC;

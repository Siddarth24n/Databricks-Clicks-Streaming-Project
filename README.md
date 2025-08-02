# Real-Time Clickstream Streaming Pipeline with Databricks

## About the Project

This is a hands-on project I created to explore how **real-time data pipelines** work using **Databricks Structured Streaming** and **Delta Lake**. I wanted to simulate how websites track user activity — like clicks on pages — and see how to ingest, process, and analyze that data as it arrives in real time.

Instead of relying on external tools like Kafka or Azure Event Hub, I used **DBFS (Databricks File System)** to keep things simple and accessible, especially since I’m using Databricks on the Standard Tier.

---

## Why I Built This

As someone diving deeper into data engineering, I really wanted to understand how **streaming pipelines** work — not just in theory, but by building something end to end.

This project helped me:
- Get hands-on with **Structured Streaming** in Spark
- Understand how **Delta Lake** handles continuous data writes
- Simulate a real-time use case without needing a big infrastructure setup
- Practice querying and analyzing **live data** using SQL

---

## Real-World Use Cases

Here are a few practical ways a pipeline like this could be used:

- **Clickstream analytics**: Track which pages users visit on a website in real time
- **User behavior tracking**: Spot patterns and optimize user flows
- **Live dashboards**: Show trending products or most viewed content
- **Fraud detection**: Alert when abnormal activity patterns occur

---

## Tech Stack

- **Databricks** (Standard Tier)
- **PySpark Structured Streaming**
- **Delta Lake**
- **DBFS (Databricks File System)**
- **Python** (for simulating click events)
- **Spark SQL**

---

## How It Works (Architecture)

notebooks/
└── clickstream_pipeline.ipynb ← Here all steps are combined: simulate, stream, query

sample-data/
└── sample_event.json

README.md

---

## 🧪 What a Sample Event Looks Like

```json
{
  "user_id": "bob",
  "page": "product",
  "timestamp": "2025-08-02T15:03:11.632Z"
}

a. Created a Small Cluster in Databricks using a lightweight VM in Single Node mode.

b. This notebook handles everything like:
Simulating the clickstream JSON files (written every 2 seconds)
Ingests those files using Structured Streaming
Cleans and stores the output in Delta format
and query the output in real time

c. We can query the processed Delta table using Spark SQL. For example:
-- Total views per page
SELECT page, COUNT(*) AS views
FROM clickstream_data
GROUP BY page
ORDER BY views DESC;


Some of the Fun Queries:

-- Who are the most active users?
SELECT user_id, COUNT(*) AS events
FROM clickstream_data
GROUP BY user_id
ORDER BY events DESC;

-- What’s happening right now?
SELECT *
FROM clickstream_data
ORDER BY timestamp DESC
LIMIT 10;



-Siddarth N
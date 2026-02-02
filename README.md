# **📰 News Data Analytics Platform (Microsoft Fabric)** 

### 📌 Overview

This project implements an end-to-end news data analytics platform that
ingests real-time news data from a REST API, processes it using
Microsoft Fabric, enriches it with sentiment analysis, and delivers
insights through Power BI dashboards and Teams alerts.

The platform is designed to support incremental data processing,
scalable transformations, and real-time sentiment monitoring of U.S.
news articles.

### 🎯 Use Case

-   Track the top 100 news articles in the U.S. from the last 24 hours

-   Analyze sentiment trends (Positive / Neutral / Negative)

-   Enable real-time alerts when positive news is detected

-   Provide an analytics-ready semantic model for reporting

### 🛠️ Tech Stack

-   Microsoft Fabric

-   Data Pipelines

-   Lakehouse (Files & Tables)

-   Notebooks (PySpark)

-   REST API

-   Brave Search News API

-   Machine Learning

-   SynapseML (analyzeText for sentiment analysis)

-   Analytics & Visualization

-   Power BI

-   DAX

-   Notifications

-   Microsoft Teams Alerts

### 🏗️ Architecture 

<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/91d07cae-34c6-41c0-b5f0-6167ba626345" />


### 🔄 Data Pipeline Flow 

1.   **News Data Ingestion**

-   Used Copy Data activity to fetch news articles from Brave Search API

-   Parameterized API URL to support topic-based filtering

-   Default configuration retrieves top 100 U.S. news articles from the
    past 24 hours

-   Stored raw response as JSON files in the Lakehouse

📂 Lakehouse: News_Lake_DB (Files)

2.   **Data Processing & Transformation**

-   Notebook: process_news_data.ipynb

-   Key transformations:

    -   Parsed nested JSON response using PySpark

    -   Standardized datePublished format

    -   Cleaned and normalized category and provider fields

    -   Removed invalid or malformed records

    -   Selected analytics-ready columns

-   Incremental load strategy:

    -   Type 1 Merge

    -   Target table: tbl_latest_news

3.   **Sentiment Analysis**

Notebook: news_sentiment_analysis.ipynb

-   Used SynapseML AnalyzeText model

-   Performed sentiment analysis on the description column

-   Generated sentiment scores and labels:

    -   Positive

    -   Neutral

    -   Negative

-   Cleaned and restructured output

-   Incremental load:

    -   Type 1 Merge

    -   Target table: tbl_sentiment_analysis

### 📊 Reporting & Analytics (Power BI)

-   Created semantic model on tbl_sentiment_analysis

-   Built Power BI report with:

-   News details table (title, datePublished, category, URL, image URL)

-   Date slicer on datePublished

-   KPI cards for:

    -   \% Positive

    -   \% Neutral

    -   \% Negative sentiment (DAX measures)

-   Applied filters to show top 2 latest news articles by publish date

### 🔔 Alerts & Automation

-   Configured Teams alerts

-   Notification triggered when:

    -   Positive sentiment news is detected

-   Enables near real-time awareness of favorable news trends

### 🚧 Challenges & Solutions 

| Challenge                   | Solution                                    |
|-----------------------------|---------------------------------------------|
| API JSON parsing issues     | Explicit schema handling in PySpark         |
| Invalid date values         | Custom date parsing and standardization     |
| Schema mismatch during load | Controlled Type 1 merge strategy            |
| Incremental processing      | Merge-based upserts instead of full reloads |

### 🚀 Future Enhancements

-   Topic-based sentiment comparison

-   Historical trend analysis

-   Entity recognition (companies, locations)

-   Streaming ingestion using Eventstreams

### 

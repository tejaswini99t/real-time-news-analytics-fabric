## Power BI Report Overview

This Power BI report is built on top of the Fabric semantic model created from `tbl_sentiment_analysis`.

### Key Features
- News details table:
  - Title
  - Date Published
  - Category
  - URL
  - Image URL
- Date slicer on `datePublished`
- KPI cards:
  - % Positive sentiment
  - % Neutral sentiment
  - % Negative sentiment
- Filter to show top 2 latest news articles by publish date
- Alert configured to notify Microsoft Teams when positive sentiment is detected

### Notes
- PBIX uses a Fabric semantic model as the data source
- No credentials or secrets are stored in this file

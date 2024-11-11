# Full Analytics Engineer Project in Microsoft Fabric for Bing News API (US Election News in Australia)
![image](https://github.com/user-attachments/assets/11ce83b1-a3de-4a7d-b5bb-c72b047fbdbd)

## Project Overview

In this project, I’m building a comprehensive data pipeline and analytics solution using Microsoft Fabric to collect, process, analyze, and visualize news data related to the US election, specifically focusing on how the election is covered in Australia. The goal is to create an end-to-end system that automatically ingests the latest news, processes and transforms that data, performs sentiment analysis to assess the tone of each news article, and then visualises the results through an interactive dashboard. Additionally, I’ll configure real-time alerts based on sentiment, sending notifications to Microsoft Teams whenever a negative sentiment is detected.
The project will be divided into five major steps. I will utilise various tools within Microsoft Fabric, including Data Factory, Synapse Data Engineering, Synapse Data Scientist, Power BI, and Data Activator. Using the Bing News API, I'll gather raw data, clean and transform it, run sentiment analysis, create a dashboard for monitoring trends, and configure real-time alerts.


## Tools and Technologies

### Microsoft Fabric:
- **Data Factory**: For data ingestion and ETL processes.
- **Synapse Data Engineering**: For data transformation with Spark notebooks.
- **Synapse Data Science**: For sentiment analysis using a text analytics ML model.
- **Power BI**: For creating data visualisations and dashboards.
- **Data Activator**: For setting up real-time alerts based on sentiment.

### External Data Source:
- **Bing News API**: For fetching the latest news articles related to the US election in Australia.

## Analytics Engineering Technical Skills

### Analytics Engineering Technical Skills

**Data Ingestion**  
Data Pipeline: Azure Data Factory, incremental load, scheduled refresh  

**Data Transformation & Pipeline**  
PySpark: Transforming raw JSON data, Synapse Data Engineering for data processing and optimisation, automated pipelines with Azure Data Factory  

**Cloud Data Management & Storage**  
OneLake, Lakehouse architectures: Storing raw JSON data in Lakehouse, transforming to Delta tables for optimised queries  

**Data Science & Sentiment Analysis**  
PySpark, Synapse Data Science: Text analytics, sentiment analysis (positive, negative, neutral) using ML models  

**Data Warehousing & Analytics**  
Delta Lake: Building and managing data warehouses for analytics reporting  

**Power BI Data Visualisation**  
Power BI: Data gathering, Power Query, Data Modelling, Report Design, DAX, business and analytics reporting, performance optimisation, deployment to Power BI Service, scalability  

**Continuous Improvement**  
Optimising ETL processes, scaling data pipelines and reports, monitoring workflows for performance improvements and data accuracy  

**Real-time Alerts & Monitoring**  
Data Activator: Configuring real-time alerts based on sentiment thresholds, integrating with Microsoft Teams for automated notifications  

# Data Engineering Process

### Environment Setups
I created a resource group called `rg-fabric-bing-analytics` and used the marketplace to search for the Bing Search v7 API to create a Bing Search resource. I selected the **F1** pricing tier (3 calls per second and 1,000 calls per month) because it is free.









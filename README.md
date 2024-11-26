# End-to-End Analytics Project by Microsoft Fabric for Latest AI News (Bing API News)
![image](https://github.com/user-attachments/assets/f3c26dce-6362-4c74-8958-567a5be01640)


## Project Overview
In this project, I’m building a comprehensive data pipeline and analytics solution using Microsoft Fabric to collect, process, analyse, and visualise AI news data in Australia. The goal is to create an end-to-end system that automatically ingests the latest news in AI, processes and transforms that data, performs sentiment analysis to assess the tone of each news article, and then visualises the results through an interactive dashboard. Additionally, I’ll configure real-time alerts based on sentiment, sending notifications to Microsoft Teams whenever a negative sentiment is detected.
The project will be divided into five major steps. I will utilise various tools within Microsoft Fabric, including Data Factory, Synapse Data Engineering, Synapse Data Scientist, Power BI, and Data Activator. Using the Bing News API, I'll gather raw data, clean and transform it, run sentiment analysis, create a dashboard for monitoring trends, and configure real-time alerts.


## Tools and Technologies

### Microsoft Fabric:
- **Data Factory**: For data ingestion and ETL processes.
- **Synapse Data Engineering**: For data transformation with Spark notebooks.
- **Synapse Data Science**: For sentiment analysis using a text analytics ML model.
- **Power BI**: For creating data visualisations and dashboards.
- **Data Activator**: For setting up real-time alerts based on sentiment.

### External Data Source:
- **Bing News API**: For fetching the latest AI news in Australia.


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

### Data Ingestion
I created a lakehouse called `Bing_LH` to configure both the source and destination for data ingestion.

#### Source Configuration:
- Design a pipeline in Data Factory to fetch data from Bing News.
- Use the Copy Data activity to move data from the Bing News API to OneLake.
- Set up a connection to the Bing News API using the REST API in the Data Factory.
- Configure the API with necessary parameters such as query, filters, and API key. The query parameter retrieves up to 100 news articles published within 24 hours and ensures the results are from Australia.
[View the Query Parameter Sample](https://github.com/NilooKandi/Fabric-Analytics-Bing-News-Search/blob/main/Query%20Parameter.md)

#### Destination Configuration:
- The destination is set to the `Bing_LH` lakehouse.
- A file path called `bing-news.json` is created.
- The file format is set to **JSON**.

### Data Transformation with Incremental Loading
I used a Spark notebook to process the raw JSON file and transform it into a clean Delta table.
















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

#### Parameter Configuration

I configured a parameter to make the pipeline more flexible by enabling it to accept different input values for each execution. This adaptability allows the pipeline to handle a variety of scenarios without the need to redesign it for each specific use case. Such a configuration is particularly useful in data integration, transformation, and orchestration tasks
![image](https://github.com/user-attachments/assets/969ff858-4fab-4ca1-adee-d3e59ea5fdb3)

#### Destination Configuration:
- The destination is set to the `Bing_LH` lakehouse.
- A file path called `bing-news.json` is created.
- The file format is set to **JSON**.

### Data Transformation with Incremental Loading
I used a Spark notebook to process the raw JSON file and transform it into a clean Delta table.

- [View ETL process here ](https://github.com/NilooKandi/Fabric-Analytics-Bing-AI-News-Search/blob/main/process_bing_latest_AI_news.ipynb)

# Data Science Process
### Sentiment Analysis with Incremental Loading

For sentiment analysis, I leveraged SynapseML (previously known as MMLSpark), which is integrated into Microsoft Fabric. This open-source library provides pre-trained models for machine-learning tasks. In this case, I used its sentiment analysis capabilities to evaluate the emotional tone of AI news articles, processing the detailed descriptions in our news dataset to determine their sentiment.

- [View Sentiment Analysis here ](https://github.com/NilooKandi/Fabric-Analytics-Bing-AI-News-Search/blob/main/news_sentiment_analysis.ipynb)

## Building Pipelines using Data Factory for Orchestration

![image](https://github.com/user-attachments/assets/8afd382d-5145-4208-acdd-1efd02ab1700)

To maintain up-to-date news analysis, I implemented an automated refresh schedule in Data Factory that runs daily at 8:00 AM. This scheduled refresh executes three components sequentially:

1. The data ingestion pipeline
2. The ETL_process_AI_news notebook for data processing
3. The AI_news_sentiment_analysis notebook for sentiment evaluation

This automation ensures we have fresh insights from the latest news data each morning.
![image](https://github.com/user-attachments/assets/7dee3066-eff4-497d-a19b-25766848d783)


## Data Visualisation in Power BI

-[View KPIs here](https://github.com/NilooKandi/Fabric-Analytics-Bing-AI-News-Search/tree/main)

<img width="1192" alt="Screenshot 2024-12-27 173624" src="https://github.com/user-attachments/assets/a22e6cca-771d-4944-b29c-c77df287990c" />










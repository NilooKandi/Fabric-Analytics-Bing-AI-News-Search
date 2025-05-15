# DATA TRANSFORMATION OF AI NEWS JSON DATA

```python
df = spark.read.option("multiline", "true").json("Files/bing-news.json")
display(df)
```

```python
#display only the news article which is in the value Column above.
df = df.select("value")
display(df)
```

```python
""" The explode import allow us to Returns a new row for each element in the given array or map.
exploring the json to covert column to multiple rows."""

from pyspark.sql.functions import explode
#'json_object' is the field we want to explode
df_expload = df.select(explode(df["value"]).alias('json_object'))

display(df_expload)
```

```python
#convert json dataframe to a single json string list
json_list = df_expload.toJSON().collect()

print(json_list[1])
```

Output:
```
{"json_object":{"about":[{"name":"Artificial intelligence","readLink":"https://api.bing.microsoft.com/api/v7/entities/9d99fb44-edac-0e03-1579-19d8d8591a49"},{"name":"Computer science","readLink":"https://api.bing.microsoft.com/api/v7/entities/9aacccba-f63c-1392-c63b-48c58a98729a"}],"datePublished":"2024-12-26T07:27:00.0000000Z","description":"Recruitment experts say pulling a stunt like ours for real might be tempting in a hyper-competitive jobs market where hundreds, if not thousands of people are going for the same job.","image":{"thumbnail":{"contentUrl":"https://www.bing.com/th?id=OVFT.R0kM4NiwfV3I8ycH1JiZRy&pid=News","height":393,"width":700}},"name":"I used AI to write my CV to apply for jobs I could never do - I got interested employers asking me to get in touch with them after just 30 MINUTES","provider":[{"_type":"Organization","image":{"thumbnail":{"contentUrl":"https://www.bing.com/th?id=ODF._kZMPt4WNJFUpf58U6Qe-w&pid=news"}},"name":"Daily Mail"}],"url":"https://www.dailymail.co.uk/news/article-14110877/ai-write-cv-jobs-employers-recruitment.html"}}
```

```python
# convert the json list to a json dictionary to easily process data.

import json
news_json = json.loads(json_list[1])

print(news_json)
```

Output:
```
{'json_object': {'about': [{'name': 'Artificial intelligence', 'readLink': 'https://api.bing.microsoft.com/api/v7/entities/9d99fb44-edac-0e03-1579-19d8d8591a49'}, {'name': 'Computer science', 'readLink': 'https://api.bing.microsoft.com/api/v7/entities/9aacccba-f63c-1392-c63b-48c58a98729a'}], 'datePublished': '2024-12-26T07:27:00.0000000Z', 'description': 'Recruitment experts say pulling a stunt like ours for real might be tempting in a hyper-competitive jobs market where hundreds, if not thousands of people are going for the same job.', 'image': {'thumbnail': {'contentUrl': 'https://www.bing.com/th?id=OVFT.R0kM4NiwfV3I8ycH1JiZRy&pid=News', 'height': 393, 'width': 700}}, 'name': 'I used AI to write my CV to apply for jobs I could never do - I got interested employers asking me to get in touch with them after just 30 MINUTES', 'provider': [{'_type': 'Organization', 'image': {'thumbnail': {'contentUrl': 'https://www.bing.com/th?id=ODF._kZMPt4WNJFUpf58U6Qe-w&pid=news'}}, 'name': 'Daily Mail'}], 'url': 'https://www.dailymail.co.uk/news/article-14110877/ai-write-cv-jobs-employers-recruitment.html'}}
```

```python
#syntax to drill in using a dictionary
print (news_json['json_object']['description'])
```

Output:
```
Recruitment experts say pulling a stunt like ours for real might be tempting in a hyper-competitive jobs market where hundreds, if not thousands of people are going for the same job.
```

```python
# Print the keys (headers) of the top-level dictionary
print(news_json.keys())
```

Output:
```
dict_keys(['json_object'])
```

```python
#  To see want to see the keys inside the 'json_object' (the nested dictionary)
print(news_json['json_object'].keys())
```

Output:
```
dict_keys(['about', 'datePublished', 'description', 'image', 'name', 'provider', 'url'])
```

```python
#get specific items from the json dictionary (description of the news)

print(news_json["json_object"]["name"])  
print(news_json["json_object"]["description"])
print(news_json["json_object"]["image"]["thumbnail"]["contentUrl"])
print(news_json["json_object"]["datePublished"])
print(news_json["json_object"]["provider"][0]["name"])
print(news_json["json_object"]["url"])
```

Output:
```
I used AI to write my CV to apply for jobs I could never do - I got interested employers asking me to get in touch with them after just 30 MINUTES
Recruitment experts say pulling a stunt like ours for real might be tempting in a hyper-competitive jobs market where hundreds, if not thousands of people are going for the same job.
https://www.bing.com/th?id=OVFT.R0kM4NiwfV3I8ycH1JiZRy&pid=News
2024-12-26T07:27:00.0000000Z
Daily Mail
https://www.dailymail.co.uk/news/article-14110877/ai-write-cv-jobs-employers-recruitment.html
```

```python
#Process json property to List
title = []
description = []
image = []
link = []
datePublished = []
provider = []


#Process each JSON object iun the list
for json_string in json_list:
    try:
        #parse the JSON string into a dictionary
        item = json.loads(json_string)

        #Extract information from the dictionary
        title.append(item["json_object"]["name"])
        description.append(item["json_object"]["description"])
        image.append(item["json_object"]["image"]["thumbnail"]["contentUrl"])
        link.append(item["json_object"]["url"])
        datePublished.append(item["json_object"]["datePublished"])
        provider.append(item["json_object"]["provider"][0]["name"])
    
    except Exception as e:
        print(f"Error processing JSON field: {e}")
```

Output:
```
Error processing JSON field: 'image'
Error processing JSON field: 'image'
Error processing JSON field: 'image'
Error processing JSON field: 'image'
Error processing JSON field: 'image'
Error processing JSON field: 'image'
Error processing JSON field: 'image'
Error processing JSON field: 'image'
```

```python
#THE IF STATEMENT = Don't process any item whose details is not in the json list 
#with this, the Error above is mitigated

title = []
description = []
image = []
link = []
datePublished = []
provider = []

#Process each JSON object iun the list
for json_string in json_list:
    try:
        #parse the JSON string into a dictionary
        item = json.loads(json_string)

        # This to remove all news that has no images attched to it.
        if item["json_object"].get("image", {}).get("thumbnail", {}).get("contentUrl"):

            #Extract information from the dictionary
            title.append(item["json_object"]["name"])
            description.append(item["json_object"]["description"])
            image.append(item["json_object"]["image"])
            link.append(item["json_object"]["url"])
            datePublished.append(item["json_object"]["datePublished"])
            provider.append(item["json_object"]["provider"][0]['name'])
    
    
    except Exception as e:
        print(f"Error processing JSON field: {e}")
```

```python
#Convert List to a DataFrame
from pyspark.sql.types import StructType, StructField, StringType

#combine all list
AI_news_data = list(zip(title,description,image,link,datePublished, provider))

#Define Schema
schema = StructType([
    StructField("title", StringType(), True),
    StructField("description", StringType(), True),
    StructField("image", StringType(), True),
    StructField("link", StringType(), True),
    StructField("datePublished", StringType(), True),
    StructField("provider", StringType(), True),
    
])
#create DataFrame
df_clean = spark.createDataFrame(AI_news_data, schema=schema)
```

```python
#Lets look at the cleaned data
display(df_clean)
```

```python
#Split datePublished into Date and Time columns 
from pyspark.sql.functions import col, date_format

df_clean = df_clean.withColumn("published_date", date_format(col("datePublished"), "yyyy-MM-dd"))
df_clean = df_clean.withColumn("published_time", date_format(col("datePublished"), "HH:mm:ss"))

display(df_clean)
```

```python
# Convert published_date column to Date data type
 
from pyspark.sql.functions import to_date, date_format

df_clean_final = df_clean.withColumn("published_date", to_date(col("published_date"), "yyyy-MM-dd"))

display(df_clean_final)
```

## Writing the final Dataframe to the Lakehouse DB in Delta Format

```python
df_clean_final.write.format("delta").saveAsTable('bing_LH.tbl_latest_AI_news')
```

## Implementing the Type 1 incremental Loading of the Transformed Data

```python
# Adopting TYPE 1 SCD incremental loading for our data.

'''In a Type 1 SCD the new data overwrites the existing data without duplicate. Thus the existing data
 is lost as it is not stored anywhere else. This is typically used when there is no need to keep 
 a history of the data.'''

from pyspark.sql.utils import AnalysisException

#Exception Handling
try:

    table_name = "bing_LH.tbl_latest_AI_news"
    df_clean_final.write.format("delta").saveAsTable(table_name)

except AnalysisException:

    print ("Table Already Exist")

    df_clean_final.createOrReplaceTempView("vw_df_clean_final")

    spark.sql(f"""  MERGE INTO {table_name} target_table
                    USING vw_df_clean_final source_view

                    ON source_view.link = target_table.link

                    WHEN MATCHED AND
                    source_view.title <> target_table.title OR
                    source_view.description <> target_table.description OR
                    source_view.image <> target_table.image OR
                    source_view.link <> target_table.link OR
                    source_view.datePublished <> target_table.datePublished OR
                    source_view.provider <> target_table.provider OR
                    source_view.published_date <> target_table.published_date OR
                    source_view.published_time<> target_table.published_time
                    
                    THEN UPDATE SET *

                    WHEN NOT MATCHED THEN INSERT * 

                """)
```

Output:
```
Table Already Exist
```

```sql
-- This is to count the number of data was loaded into the Lakehouse

SELECT COUNT(*) FROM bing_LH.tbl_latest_AI_news
```

Result: 40 rows


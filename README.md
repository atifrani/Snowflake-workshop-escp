# Snowflake-labs

##  Sign Up for a Snowflake Trial Account on AWS:

Please use this link to sign up for a trial account: https://signup.snowflake.com/?trial=student&cloud=aws&region=us-west-2&utm_source=handsonessentials&utm_campaign=uni-dww#

The link above will ensure that you use the right settings as well as giving you 120 days instead of the standard 30 days. 

## 🚨 Choose Your Snowflake Password Carefully
* We have seen issues with Usernames or Passwords that contain accented characters when making some database connections. 
* Avoid this issue and don't include accented characters in your username or password when creating your trial account!

### Find the Email from Snowflake & Activate Your Account.

![alt text](images/img1.png)

## Log in to your Snowflake Trial

When you activated your account it would have opened your trial in a new browser tab, but just in case you closed that tab or lost track of it, remember you can always go back to your email inbox and find an email that will give you the link to your Snowflake Trial account. 

![alt text](images/img2.png)

## Create a New Database:

![alt text](images/img3.png)

![alt text](images/img4.png)

### Switch Your System Role to SYSADMIN

![alt text](images/img5.png)

Notice that the DEMO_DB has disappeared from your list of databases. 

![alt text](images/img6.png)

###  Switch Your System Role Back to ACCOUNTADMIN.

![alt text](images/img7.png)

The DEMO_DB database reappears. It is only available to the ACCOUNTADMIN role, not the SYSADMIN role. 

### Explore the Database You Created

![alt text](images/img8.png)

### Organizing Database Objects
Databases are used to group datasets (**tables**) together. A second-level organizational grouping, within a database, is called a schema. 

* Every time you create a database, Snowflake will automatically create two schemas for you.

* The **INFORMATION_SCHEMA** schema holds a collection of views.  The INFORMATION_SCHEMA schema cannot be deleted (dropped), renamed, or moved.

* The **PUBLIC** schema is created empty and you can fill it with tables, views and other things over time. The PUBLIC schema can be dropped, renamed, or moved at any time.  

### Transfer Ownership of Your Database to the SYSADMIN Role

![alt text](images/img9.png)

![alt text](images/img10.png)

![alt text](images/img18.png)

### Switch Your System Role Back to SYSADMIN

![alt text](images/img11.png)

Can you see DEMO_DB now that SYSADMIN owns it?


### Learning About Snowflake System Roles

![alt text](images/img12.png)

### Warehouses in Your Trial Account
In Snowflake, data is held in databases and any processing of data is done by something called a "**warehouse**." Most people who work in the data field think of a **warehouse** as a special kind of **database**, not as a **compute engine**. Only Snowflake calls computing engines "warehouses."   

Regardless of the terminology, when your trial account was created, three compute resources (a.k.a "warehouses") were created for you. 

One is called **SNOWFLAKE_LEARNING_WH**. It's owned by **ACCOUNTADMIN**.  You will use the **SNOWFLAKE_LEARNING_WH** warehouse to do your lab work in this workshop.

![alt text](images/img13.png)

### Make the Warehouse Available to SYSADMIN 

There are different ways to make a compute resource available to different roles, but as we saw with databases, sometimes the easiest way to grant access is to transfer ownership to a lower role.  Since the ACCOUNTADMIN role is in the same tree as the SYSADMIN role, ACCOUNTADMIN will still have access to the warehouse, even if SYSADMIN is the owner. 

![alt text](images/img14.png)



### Create a Worksheet & Run Some Code

 Snowflake now offers SQL and Python Worksheets. Please choose SQL Worksheets throughout this course. 

![alt text](images/img15.png)

![alt text](images/img16.png)


### Worksheet Context Menus
Every worksheet has 4 drop menus near the top. Two are in the upper right corner and two are close to the first line of code. Which two are near the code? Which two are in the upper right corner? 

![alt text](images/img17.png)


### Load Data manually:

### Load structured Data:

1. Click on this link https://github.com/atifrani/Snowflake-workshop-escp/blob/main/Data/employees.csv to download the data localy in you machine.
2. Open a new SQL worksheet and rename the worksheet **load-empolyees-csv.sql**
3. Create employees-csv table, copy the script bellow and run it.

```
USE ROLE SYSADMIN;

USE WAREHOUSE SNOWFLAKE_LEARNING_WH;

USE DATABASE DEMO_DB;

USE SCHEMA PUBLIC;

CREATE OR REPLACE TABLE EMPLOYEES_CSV
(
emp_id varchar,
fname varchar,
lname varchar,
adress varchar,
city varchar,
state varchar,
zipcode varchar,
job_title varchar,
email varchar,
active boolean,
salary int
);
```
4. Add data to tables through the Console web interface

![alt text](images/img19.png)

![alt text](images/img20.png)

![alt text](images/img21.png)

![alt text](images/img22.png)

![alt text](images/img23.png)

5. Query your data

```
SELECT * FROM EMPLOYEES_CSV;
```

![alt text](images/img24.png)


### Load semi-structured Data:

1. Click on this link https://github.com/atifrani/Snowflake-workshop-escp/blob/main/Data/employees.json to download the data localy in you machine.
2. Open a new SQL worksheet and rename the worksheet **load-empolyees-json.sql**
3. Create employees-json table, copy the script bellow and run it.

```
USE ROLE SYSADMIN;

USE WAREHOUSE SNOWFLAKE_LEARNING_WH;

USE DATABASE DEMO_DB;

USE SCHEMA PUBLIC;

CREATE OR REPLACE TABLE EMPLOYEES_JSON
(
V VARIANT
);
```
4. Add data to tables through the Console web interface

![alt text](images/img25.png)

![alt text](images/img26.png)

![alt text](images/img28.png)

![alt text](images/img29.png)

4. Query your data

```
SELECT * FROM EMPLOYEES_JSON;
```

![alt text](images/img30.png)

6. Querying Semi-Structured Data

```
Select 
    V:emp_id ,
    V:fname ,
    V:lname ,
    V:adress ,
    V:city ,
    V:state ,
    V:zipcode ,
    V:job_title ,
    V:email ,
    V:active ,
    V:salary 
from EMPLOYEES_JSON;
```
7. Convert Semi-Structured data to Structured data.

```
CREATE OR REPLACE VIEW EMPLOYEES_VIEW
AS
Select 
    V:emp_id ,
    V:fname ,
    V:lname ,
    V:adress ,
    V:city ,
    V:state ,
    V:zipcode ,
    V:job_title ,
    V:email ,
    V:active ,
    V:salary 
from EMPLOYEES_JSON;
```
8. Query your data from the view:

```
SELECT * FROM EMPLOYEES_VIEW
```

## 🔍 Workshop Introduction: Become an Analytics Engineer at Airbnb (Berlin)

Welcome to this hands-on workshop! You’ll step into the role of an **Analytics Engineer at Airbnb**, responsible for managing and transforming data specifically for the **Berlin, Germany** market.

As an analytics engineer, you’ll be in charge of overseeing the entire data pipeline—from ingesting raw data to delivering actionable insights through BI tools. This is a critical responsibility, and you'll be guiding data through several key stages:

1. **Importing** raw data into a data warehouse
2. **Cleansing** and **transforming** the data to make it analytics-ready
3. **Exporting** the processed data into a BI tool for visualization and decision-making

Throughout the workshop, I’ll walk you through each step, ensuring you understand both the tools and the concepts behind them.

The dataset we'll be using is **real and reliable**, sourced directly from Airbnb’s open data portal:
👉 **[Inside Airbnb – Berlin](https://insideairbnb.com/berlin/)**

To make things easier, we’ve already downloaded and preprocessed the dataset for you. It’s ready to be imported into our cloud data platform.

### 🧰 Tech Stack Overview

Here are the tools and platforms we’ll be working with:

* **AWS S3** – for cloud-based data lake storage
* **Snowflake** – as our cloud data warehouse
* **Tableau** – for building interactive BI dashboards

By the end of this workshop, you’ll have a solid understanding of how a modern data pipeline functions—from ingestion to insight—using a real-world Airbnb dataset.

![alt text](images/lab-architecture.png)


### Step 1: 
To start, open a new SQL worksheet and rename it **load-airbnb-data.sql**.
let's set role and warehouse context.
**To run a single query, place your cursor in the query editor and select the Run button**

* Set Role Context:
```
USE ROLE ACCOUNTADMIN;
```

* Set Warehouse Context:
```
USE WAREHOUSE SNOWFLAKE_LEARNING_WH;
```

### Step 2:
Now, let's create Database and tables

* Create airbnb database:
```
CREATE OR REPLACE DATABASE AIRBNB;
```

* Set the Database
```
USE DATABASE AIRBNB;
```

* Create Bronze SCHEMA:
```
CREATE SCHEMA BRONZE;
```

* Set the SCHEMA
```
USE SCHEMA BRONZE;
```

* Create tables:

![alt text](images/data_model.png)

Before creating tables, take time to understand the structure of each file.

```
CREATE OR REPLACE TABLE bronze.raw_hosts
                    (id integer,
                     name string,
                     is_superhost string,
                     created_at datetime,
                     updated_at datetime);
```

```
CREATE OR REPLACE TABLE bronze.raw_reviews
                    (listing_id integer,
                     date datetime,
                     reviewer_name string,
                     comments string,
                     sentiment string);
```

```
CREATE OR REPLACE TABLE bronze.raw_listings 
                    (data VARIANT
                    );
```

The **VARIANT** data type in Snowflake stores semi-structured data like JSON, Avro, or XML. It allows flexible schema-on-read access to nested or dynamic content without predefined structure.

### Step 3: 
Create Stage objects. 
A stage specifies where data files are stored. In our case the files are stored in S3 bucket **escp-snowflake-lab-2025**

![alt text](images/airbnb-files.png)

```
CREATE OR REPLACE STAGE airbnb_stage
  URL = 's3://escp-snowflake-lab-2025/data/'
  STORAGE_PROVIDER = 'S3'
  STORAGE_ALLOWED_LOCATIONS = ('s3://escp-snowflake-lab/');
```

* View our Stages:

```
SHOW STAGES;
```

```
LIST @airbnb_stage;
```

### Step 4: 
Load data from the Amazon S3 Stage into the Table


* Load Data into table raw_hosts:  

```
COPY INTO raw_hosts
FROM @airbnb_stage/raw_hosts.csv
FILE_FORMAT = (TYPE = 'CSV' SKIP_HEADER = 1 FIELD_OPTIONALLY_ENCLOSED_BY = '"');
```
* Start querying your Data
```
select * from raw_hosts
```

* Load Data into table raw_reviews:  

```
COPY INTO raw_reviews
FROM @airbnb_stage/raw_reviews.csv
FILE_FORMAT = (TYPE = 'CSV' SKIP_HEADER = 1 FIELD_OPTIONALLY_ENCLOSED_BY = '"');
```

* Start querying your Data
```
select * from raw_reviews;
```

* Load Data into table raw_listings:  

```
COPY INTO raw_listings
FROM @airbnb_stage/raw_listings.json
FILE_FORMAT = (TYPE ='JSON');
```
* Start querying your Data
```
select * from raw_listings;
```

### Step 5: 
Now, we need to clean the data and apply some transformations.
Create a new SQL worksheet and rename it **transform-airbnb-data.Sql**.

* Set Role Context:
```
USE ROLE ACCOUNTADMIN;
```

* Set Warehouse Context:
```
USE WAREHOUSE SNOWFLAKE_LEARNING_WH;
```

* Set the Database
```
USE DATABASE AIRBNB;
```

* Create SILVER SCHEMA:
```
CREATE SCHEMA SILVER;
```

* Set the SCHEMA
```
USE SCHEMA SILVER;
```

* Create table HOSTS:

```
CREATE OR REPLACE TABLE hosts 
AS
SELECT
    id AS host_id,
    name AS host_name,
    is_superhost::BOOLEAN AS is_superhost, -- convert data type
    created_at,
    updated_at
FROM bronze.raw_hosts;
```

* Query table HOSTS:

```
SELECT * FROM HOSTS;
```

* Create table REVIEWS:

```
CREATE OR REPLACE TABLE reviews 
AS
SELECT
    listing_id,
    date as review_date,
    reviewer_name,
    comments as review_text, -- rename column
    sentiment
FROM bronze.raw_reviews;
```
* Query table REVIEWS:

```
SELECT * FROM REVIEWS;
```

* Create table LISTINGS:

```
CREATE OR REPLACE TABLE LISTINGS 
AS
SELECT
    data:ID::INT AS id,
    data:LISTING_URL::STRING AS listing_url,
    data:NAME::STRING AS name,
    data:ROOM_TYPE::STRING AS room_type,
    data:MINIMUM_NIGHTS::INT AS minimum_nights,
    data:HOST_ID::INT AS host_id,
    data:PRICE::STRING AS price,
    data:CREATED_AT::TIMESTAMPTZ AS created_at,
    data:UPDATED_AT::TIMESTAMPTZ AS updated_at
FROM bronze.raw_listings;
```

* Query table LISTINGS:

```
SELECT * FROM LISTINGS;
```

### Step 6: 

Now that we have the complete dataset, let's develop a data model to support our analytics.

![alt text](images/data_model_silver.png)

* Create table DIM_HOSTS

```
CREATE OR REPLACE VIEW DIM_HOSTS AS
SELECT
    host_id::INT AS host_id,
    NVL(host_name::STRING, 'Anonymous') AS host_name,
    IS_SUPERHOST::BOOLEAN AS IS_SUPERHOST,
    CREATED_AT::TIMESTAMPTZ AS CREATED_AT,
    UPDATED_AT::TIMESTAMPTZ AS UPDATED_AT
FROM HOSTS;
```
* Query table DIM_HOSTS

```
Select * from DIM_HOSTS;
```

* Create table DIM_LISTINGS

```
CREATE OR REPLACE VIEW DIM_LISTINGS AS
SELECT
    ID AS LISTING_ID,
    LISTING_URL,
    NAME AS LISTING_NAME,
    ROOM_TYPE,
    CASE 
        WHEN (MINIMUM_NIGHTS)::INT IS NULL THEN 1
        WHEN (MINIMUM_NIGHTS)::INT = 0 THEN 1 
        ELSE (MINIMUM_NIGHTS)::INT 
    END AS MINIMUM_NIGHTS,
    HOST_ID,
    TO_NUMBER(REPLACE(PRICE, '$', ''))::INT AS PRICE,
    CREATED_AT,
    UPDATED_AT
FROM listings;
```

* Query table DIM_LISTINGS

```
Select * from DIM_LISTINGS;
```

* Create table FACT_REVIEWS

```
CREATE OR REPLACE TABLE FACT_REVIEWS
  AS
  SELECT 
    *
  FROM reviews
  WHERE review_text IS NOT NULL
  order by review_date desc;
```

* Query table FACT_REVIEWS

```
Select * from FACT_REVIEWS;
```

* Create table FULL_MOON_DATE:

```
CREATE OR REPLACE TABLE FULL_MOON_DATE
(
    date_day date
);
```
Load data into FULL_MOON_DATE table using the snowflake web console.

### STEP 6:

Next, we'll build a data mart to examine the correlation between review sentiment (positive vs. negative) and full moon occurrences.

Create a new SQL worksheet and rename it **analyze-airbnb-data.Sql**.

* Set Role Context:
```
USE ROLE ACCOUNTADMIN;
```

* Set Warehouse Context:
```
USE WAREHOUSE SNOWFLAKE_LEARNING_WH;
```

* Set the Database
```
USE DATABASE AIRBNB;
```

* Create GOLD SCHEMA:
```
CREATE SCHEMA GOLD;
```

* Set the SCHEMA
```
USE SCHEMA GOLD;
```

* Create tabel FULL_MOON_REVIEWS

```
CREATE OR REPLACE TABLE FULL_MOON_REVIEWS
AS
SELECT 
    fr.*, 
    CASE 
        WHEN fm.date_day IS NULL THEN 'not full moon'
        ELSE 'full moon'
    END AS is_full_moon
FROM 
    SILVER.FACT_REVIEWS fr 
JOIN 
    SILVER.FULL_MOON_DATE fm 
ON 
    (TO_DATE(fr.REVIEW_DATE) = DATEADD(DAY, 1, fm.date_day));
```

* Query table FULL_MOON_REVIEWS:

```
SELECT * FROM FULL_MOON_REVIEWS;
```

```
select count(*) as nb_reviews, sentiment from FULL_MOON_REVIEWS
group by sentiment;
```

### STEP 7:

**Snowflake Cortex AI:**
Snowflake Cortex AI is a fully managed service designed to unlock the technology’s potential for everyone within an organization, regardless of their technical capabilities. It provides access to industry-leading large language models (**LLMs**), enabling users to easily build and deploy AI-powered applications.

In this blog, we explore **Cortex Analyst**, one of the superstars of the Snowflake Cortex AI family.

**Cortex Analyst:**  
Cortex Analyst enables business users to interact with structured data using natural language, allowing them to find answers faster, self-serve insights, and save valuable time.  

Let’s start with a simple example using the TRANSLATE function:

```
select SNOWFLAKE.CORTEX.TRANSLATE('Hello Everyone', '', 'fr') AS greeting;
```

The REVIEW_TEXT column in FACT_REVIEWS contains reviews in various languages. Let's first translate them into English to check if the sentiment matches the review text.

* CREATE a new WareHouse with more compute

```
CREATE OR REPLACE WAREHOUSE LARGE_COMPUTE_WH WITH
COMMENT = 'Large warehouse for cortex analyst'
    WAREHOUSE_TYPE = 'standard'
    WAREHOUSE_SIZE = 'large'
    MIN_CLUSTER_COUNT = 1
    MAX_CLUSTER_COUNT = 2
    SCALING_POLICY = 'standard'
    AUTO_SUSPEND = 60
    AUTO_RESUME = true
    INITIALLY_SUSPENDED = true;
```

* Set the warehouse

```
USE WAREHOUSE LARGE_COMPUTE_WH;
```

```
CREATE OR REPLACE TABLE FULL_MOON_REVIEWS_TRANSLATED AS
SELECT 
    LISTING_ID,
    REVIEW_DATE, 
    REVIEWER_NAME, 
    REVIEW_TEXT, 
    SNOWFLAKE.CORTEX.TRANSLATE(REVIEW_TEXT, '', 'en') AS TRANSLATED_REVIEW_TEXT,
    SENTIMENT,
    IS_FULL_MOON  
    FROM FULL_MOON_REVIEWS;
```

* Next, we'll use Snowflake Cortex's pre-trained models to generate sentiment scores for each review.

```
CREATE OR REPLACE TABLE FULL_MOON_REVIEWS_AUGMENTED AS
SELECT 
    LISTING_ID,
    REVIEW_DATE, 
    REVIEWER_NAME, 
    TRANSLATED_REVIEW_TEXT,
    SENTIMENT,
    SNOWFLAKE.CORTEX.SENTIMENT(TRANSLATED_REVIEW_TEXT) AS SENTIMENT_GENERATED,
    IS_FULL_MOON  
    FROM FULL_MOON_REVIEWS_TRANSLATED;
```

* Sentiment scores range from -1 (completely negative) to 1 (completely positive). We’ll classify them into three categories: negative (-1 to –0.3), neutral (-0.3 to 0.3), and positive (0.3 to 1).

```
select min(SENTIMENT_GENERATED), max(SENTIMENT_GENERATED) from FULL_MOON_REVIEWS_AUGMENTED;
```

```
CREATE OR REPLACE TABLE FULL_MOON_REVIEWS_AUGMENTED AS
SELECT 
    LISTING_ID,
    REVIEW_DATE, 
    REVIEWER_NAME, 
    TRANSLATED_REVIEW_TEXT,
    SENTIMENT,
    CASE 
        WHEN SNOWFLAKE.CORTEX.SENTIMENT(TRANSLATED_REVIEW_TEXT) < -0.3 THEN 'negative'
     
        WHEN SNOWFLAKE.CORTEX.SENTIMENT(TRANSLATED_REVIEW_TEXT) BETWEEN -0.3 AND 0.3  THEN 'neutral'
     
        WHEN SNOWFLAKE.CORTEX.SENTIMENT(TRANSLATED_REVIEW_TEXT) > 0.3 THEN 'positive'
    END AS  SENTIMENT_GENERATED,
    IS_FULL_MOON  
    FROM FULL_MOON_REVIEWS_TRANSLATED;
```

* Query table FULL_MOON_REVIEWS_AUGMENTED

```
SELECT * FROM FULL_MOON_REVIEWS_AUGMENTED
```

* In the following examples, we'll demonstrate how to leverage the EXTRACT_ANSWER and SUMMARIZE functions to gain more insights from our data

**EXTRACT_ANSWER:**

```
select TRANSLATED_REVIEW_TEXT,SENTIMENT_GENERATED, SNOWFLAKE.CORTEX.EXTRACT_ANSWER(TRANSLATED_REVIEW_TEXT, 'Were the guests satisfied with their stay?'):[answer] as extract_answer
from FULL_MOON_REVIEWS_AUGMENTED limit 100;
```

**SUMMARIZE:**
```
select TRANSLATED_REVIEW_TEXT, SNOWFLAKE.CORTEX.SUMMARIZE(TRANSLATED_REVIEW_TEXT) as Summary
from FULL_MOON_REVIEWS_AUGMENTED limit 100;
```



## TODO: use cortex to generate streamlit code.


## Build Data Web Apps:

**Streamlit** is an open-source Python library that makes it easy to create and share custom web apps for data analytics and data science.

We'll begin by developing our first web app based on Airbnb data.

![alt text](images/img31.png)


![alt text](images/img32.png)

* Copy and past the follwing python code in the worksheet.

```
import streamlit as st
from snowflake.snowpark.context import get_active_session


st.title(f"AIRBNB Web App")
st.write(
  """This is our first Streamlit web app 
     application baseb on AIRBNB data!
  """
)

# Get connection
session = get_active_session()

# execute sql statement
sql = f"select count(*) as NB_LISTINGS, SENTIMENT_GENERATED from  AIRBNB.GOLD.FULL_MOON_REVIEWS_AUGMENTED group by SENTIMENT_GENERATED order by NB_LISTINGS asc;"

data = session.sql(sql).collect()

# Create a simple bar chart

st.subheader("Sentiment-Based Distribution of Listings")
st.bar_chart(data=data, x="SENTIMENT_GENERATED", y="NB_LISTINGS", color="SENTIMENT_GENERATED")

st.subheader("Underlying data")
st.dataframe(data, use_container_width=True)

```

![alt text](images/img33.png)

* Next, we'll improve the bar chart by incorporating interactive filters for a more dynamic user experience.

```
import streamlit as st
from snowflake.snowpark.context import get_active_session


st.title(f"AIRBNB Web App")
st.write(
  """This is our first Streamlit web app 
     application baseb on AIRBNB data!
  """
)

# Get connection
session = get_active_session()

# Create a select box
option = st.selectbox(
     'Select the Review Name?',
( 'Michael','Daniel','Thomas','David','Anna','Laura','Alexander','Julia','Maria','Martin','Andrea','Sarah','Christian','Lisa','Alex','Simon','Mark','Chris','Paul','Stefan','Nicole','Robert'))

# execute sql statement
sql = f"select count(*) as NB_LISTINGS, SENTIMENT_GENERATED from  AIRBNB.GOLD.FULL_MOON_REVIEWS_AUGMENTED  where reviewer_name= '{option}'group by SENTIMENT_GENERATED order by NB_LISTINGS asc;"

data = session.sql(sql).collect()

# Create a simple bar chart

st.subheader("Sentiment-Based Distribution of Listings")
st.bar_chart(data=data, x="SENTIMENT_GENERATED", y="NB_LISTINGS", color="SENTIMENT_GENERATED")

st.subheader("Underlying data")
st.dataframe(data, use_container_width=True)

```
![alt text](images/img34.png)


## Reset your snowflake account

Run the scripts below to reset your account to the state required to re-run this workshop.

```
USE ROLE ACCOUNTADMIN;

USE DATABASE DEMO_DB;

USE SCHEMA PUBLIC;

DROP TABLE IF EXISTS EMPLOYEES_CSV;

DROP TABLE IF EXISTS EMPLOYEES_JSON;

DROP DATABASE IF EXISTS DEMO_DB;

USE DATABASE AIRBNB;

USE SCHEMA BRONZE;

DROP TABLE IF EXISTS RAW_HOSTS; 

DROP TABLE IF EXISTS RAW_LISTINGS; 

DROP TABLE IF EXISTS RAW_REVIEWS; 

DROP STAGE IS EXISTS AIRBNB_STAGE;

USE SCHEMA SILVER;

DROP TABLE IF EXISTS HOSTS;

DROP TABLE IF EXISTS LISTINGS; 

DROP VIEW IF EXISTS DIM_HOSTS;

DROP VIEW IF EXISTS DIML_ISTINGS; 

DROP TABLE IF EXISTS REVIEWS; 

DROP TABLE IF EXISTS FACT_REVIEWS; 

DROP TABLE IF EXISTS FULL_MOON_DATE; 

USE SCHEMA GOLD;

DROP TABLE IF EXISTS FULL_MOON_REVIEWS;

DROP TABLE IF EXISTS FULL_MOON_REVIEWS_TRANSLATED;

DROP TABLE IF EXISTS FULL_MOON_REVIEWS_AUGMENTED;

DROP DATABASE IF EXISTS AIRBNB;

DROP WAREHOUSE IF EXISTS LARGE_COMPUTE_WH;


```

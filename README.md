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
To start, let's set role and warehouse context.
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
CREAT OR REPLACE DATABASE AIRBNB;
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
A stage specifies where data files are stored. In our case the files are stored in S3 bucket **escp-snowflake-lab**

![alt text](images/airbnb-files.png)

```
CREATE OR REPLACE STAGE bronze.airbnb-stage
  URL = 's3://escp-snowflake-lab/data/';
```

* View our Stages:

```
SHOW STAGES;
```

### Step 4: 
Load data from the Amazon S3 Stage into the Table


* Load Data into table raw_hosts:  

```
COPY INTO bronze.raw_hosts
FROM @airbnb-stage/raw_hosts.csv
FILE_FORMAT = (TYPE = 'CSV' SKIP_HEADER = 1 FIELD_OPTIONALLY_ENCLOSED_BY = '"');
```
* Start querying your Data
```
select * from bronze.raw_hosts
```

* Load Data into table raw_reviews:  

```
COPY INTO bronze.raw_reviews
FROM @airbnb-stage/raw_reviews.csv
FILE_FORMAT = (TYPE = 'CSV' SKIP_HEADER = 1 FIELD_OPTIONALLY_ENCLOSED_BY = '"');
```

* Start querying your Data
```
select * from bronze.raw_reviews;
```

* Load Data into table raw_listings:  

```
COPY INTO bronze.raw_listings
FROM @my_external_csv_stage/raw_listings.json
FILE_FORMAT = (TYPE ='JSON');
```
* Start querying your Data
```
select * from bronze.raw_listings;
```

### Step 5: 
Now, we need to clean the data and apply some transformations.

* Create SLIVER SCHEMA:
```
CREATE SCHEMA SLIVER;
```

* Set the SCHEMA
```
USE SCHEMA SLIVER;
```

```
CREATE OR REPLACE TABLE silver.hosts 
AS
SELECT
    id AS host_id,
    name AS host_name,
    is_superhost::BOOLEAN AS is_superhost, -- convert data type
    created_at,
    updated_at
FROM bronze.raw_hosts;
```
```
CREATE OR REPLACE TABLE silver.reviews 
AS
SELECT
    listing_id,
    date as review_date,
    reviewer_name,
    comments as review_text, -- rename column
    sentiment
FROM bronze.raw_reviews;
```

```
CREATE OR REPLACE TABLE silver.listings 
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
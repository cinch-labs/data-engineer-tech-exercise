# Snowflake Data Engineer Tech Test

## Introduction

This assessment is designed for candidates to demonstrate their knowledge of good software and data engineering practices. The task should take 30-40 minutes to complete, we are interested in how you approach a problem, go about solving it and communicating your solution; it is not designed to catch you out.

You can use Python to generate some of the required sample data (instructions for installing python on your machine, are in the links below). Please refer to the [README.md](./README.md) for instructions.

The rest of the data will need to be fetched by building a Python script that makes an API call and stores the data into a CSV file. The details of API endpoint and response structure are both shown below as well.

### Test Instructions
The purpose of this exercise is to complete a small data pipeline in Snowflake that creates resources to warehouse data and produce an aggregate query to find useful insights.

Please fork this repo and build out your solution.

You will require a [Snowflake account](https://www.snowflake.com/), creating a trial account is free and simple to set up.

The aim of this exercise is to write code that creates a simple data warehouse in Snowflake, load the data and find the most popular products by view.


## Tech Test
User Story

> cinch has a new data source detailing which products each user has viewed in a given session. The BI team require the data to be ingested and access set up through Snowflake; after ingestion the BI team need assistance in building a view which returns the most popular vehicles by number of views. Once this report has been created, a BI team member, Rylan Clark-Neal, will require access to the view.

The input data sources are comprised of customers (in CSV format) and transactions in the form of products viewed in a session (in JSON Lines format). The Products data source will need to be created by buiding a script that makes an API call and writes the data into in a CSV file. Their details are presented below:

**Customers**  
Contains information about customers such as the customer id and the date when they joined:

| CUSTOMER_ID | AVG_VISITS_PER_MONTH |
| ----------- | ------------- |
| C1       | 7        |


    As a data scientist I want to be able to consume a data source
    that contains information about how many times each of
    our customers views our products in a given period,
    so that I can predict what they will buy next.

**Transactions**
Is an ever-increasing data source that currently contains 3 months of transactions.

Each transaction contains the customer id, details of what products they viewed and the date of the session:

```json
{
    "CUSTOMER_ID": "C1",
    "PRODUCTS_VIEWED": [
        {
            "PRODUCT_ID": "P3",
            "PRICE": 5060
        },
        {
            "PRODUCT_ID": "P4",
            "PRICE": 1210
        }
    ],
    "DATE_OF_SESSION": "2018-09-01 11:09:00"
}

```

**Note**: when uploading the files, you may wish to combine them first. Do this with a language of your choice or with Bash, use the following:

    cat **/*.json > files.json


**Products API script**  
This file will need to be created. It will contain information about products such as the product id, model and make of a vehicle:

| PRODUCT_ID | MODEL | MAKE |
| ---------- | ------------------- | ---------------- |
| P100       | DS3 | CITROEN                |

The relevant data can be retrieved by making a GET request to the following endpoint: 
    
    https://search.api.cinch.co.uk/vehicles

Build a script that loads this data into a file named 'products.csv'

### Acceptance Criteria

Create a simple data warehouse to ingest this data, create an RBAC model such that the BI team member Rylan can access the data.

Create a VIEW in Snowflake showing the Top 10 products viewed and give access to Rylan.

To arrive at this the following steps will need to be completed:

* Create a Database
* Create a Schema
* Create tables for the data concerned
* Upload the data
* Create a view for the top 10 products viewed

# Snowflake Data Engineer Tech Test

## Introduction

This assessment is designed for candidates to demonstrate their knowledge of good software and data engineering practices. The task should take 30-40 minutes to complete, we are interested in how you approach a problem, go about solving it and communicating your solution; it is not designed to catch you out.

You can use Python to generate the required sample data (instructions for installing python on your machine, are in the links below). Please refer to the [README.md](./README.md) for instructions.

You will also need to create a data source by building a Python script that makes an API call and wrangles the JSON response into a CSV file. The details of API endpoint will be mentioned below.

### Test Instructions

The purpose of this exercise is to complete a small data pipeline in Snowflake that creates resources to warehouse data and produce an aggregate query to find useful insights.

Please fork this repo and build out your solution.

You will require a [Snowflake account](https://www.snowflake.com/), creating a trial account is free and simple to set up.

The aim of this exercise is to write code that creates a simple data warehouse in Snowflake, load the data and find the most popular products by view.

## Tech Test

User Story

> cinch has a new data source detailing which products each user has viewed in a given session. The BI team require the data to be ingested and access set up through Snowflake; after ingestion the BI team need assistance in building a view which returns the most popular vehicles by number of views. Once this report has been created, a BI team member, Rylan Clark-Neal, will require access to the view.

The input data sources are comprised of customers (in CSV format), transactions in the form of products viewed in a session (in JSON Lines format) and products (in CSV format). Their details are presented below:

**Customers**  
Contains information about customers such as the customer id and the date when they joined:

| CUSTOMER_ID | AVG_VISITS_PER_MONTH |
| ----------- | -------------------- |
| C1          | 7                    |

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

**Products**  
Contains information about products such as the product id, model and make of a vehicle:

| PRODUCT_ID | MODEL | MAKE    |
| ---------- | ----- | ------- |
| P100       | DS3   | CITROEN |

**API data**

Make a GET request to the following endpoint:

    https://search-api.snc-prod.cinch.co.uk/vehicles

From the object returned by the API call, you can find the attributes required in the CSV file by accessing the following nested directory:

```
obj['facets]['makes']
```

Create and run a script that loads this data into a file named **api-data.csv**. We recommend using the '_requests_' library to make this call.

### Acceptance Criteria

Create a simple data warehouse to ingest this data.

Create a VIEW in Snowflake showing the Top 10 products viewed.

To arrive at this the following steps will need to be completed:

- Create a Database
- Create a Schema
- Create tables for the data concerned
- Upload the data
- Create a view for the top 10 products viewed

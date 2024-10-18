# dbt Transformation of Sales Data in BigQuery

## Overview
This project demonstrates how sales data was transformed using dbt on BigQuery through Google Cloud. Below are the processes and steps followed to achieve the transformation.

## Setup and Configuration

1. **Joining a dbt Cloud Project**
   - Connect dbt to BigQuery to ingest raw data from the warehouse.
   - Go to the **Connections** section in the dbt settings page to configure.
   - On Google Cloud, create a project and enable the BigQuery API.
   - Create a **Service Account** under the project and grant the following roles: 
     - BigQuery Job User 
     - BigQuery Data Editor  
   [Follow this guide to configure BigQuery and dbt](https://docs.getdbt.com/docs/get-started/connection-profiles/bigquery-setup).

2. **Version Control Setup**
   - Set up your dbt project environment.
   - Connect your **GitHub** account under **Settings > Integrations** in dbt Cloud for version control.
   - Create a branch in the GitHub repo. 
   - Use the **dbt Cloud IDE** to switch to the new branch, pull from the repo, and start development.

## Data Overview

The data was split into two datasets: 
- **Jaffle Shop Dataset**:
  1. **Customer Data**: Provides customer identification and order dates.
  2. **Orders Data**: Includes order identification, status, and placement dates.
  
- **Stripe Dataset**:
  - Contains payment data, associated orders, payment status, and amounts.

The goal was to create two tables:
1. **`dim_customers`**: Information on customers, order dates, number of orders, and lifetime value.
2. **`fct_orders`**: Details about orders, including customers, order dates, and amounts.

## Project Structure

- **dbt_project.yml**: Configures the project, including materialization settings.
  - **Staging models** are materialized as views.
  - **Marts models** are materialized as tables.
Refer to the dbt_project.yml file in the README file

### Folders in the Project

1. **models/staging**: Stages the raw data from Jaffle Shop and Stripe datasets.
2. **models/marts**: 
   - Contains **fct_orders** (in the finance section) and **dim_customers** (in the marketing section).

3. **tests**: 
   - Contains singular test files. 
   - Primary key tests and field validation tests are included in model-specific YAML files.

## Source Documentation and Testing

Sources are documented in YAML files:
- **_jaffle_shop_sources.yml** 
- **_stg_stripe_sources.yml**


These files document raw data ingested from BigQuery and ensure data freshness. [Learn more about source freshness testing here](https://docs.getdbt.com/docs/build/sources#snapshotting-source-data-freshness).

### Referential Integrity Tests
Relationship tests validate that child records have corresponding parent records. This property is referred to as "referential integrity". [See more about data tests here](https://docs.getdbt.com/reference/resource-properties/data-tests).

## Data Transformations

1. **Staging Data**
   - Light transformations on customers and orders were performed to create `stg_jaffle_shop_customers` and `stg_jaffle_shop__orders`.
   - Payment data was also staged in `stg_stripe__payments`.
  
   <img width="909" alt="stage-stripe-payemtns" src="https://github.com/user-attachments/assets/940a53f0-73f1-4911-9584-4de8d003ad09">


2. **Creating fct_orders**
   - Contains transactional data for orders, including payment details.
   - Joins were performed between `stg_jaffle_shop__orders` and `stg_stripe__payments` using CTEs.

3. **Creating dim_customers**
   - Contains customer information and order history, including lifetime value.
   - Joins were performed on customer and order data using CTEs.
  


## Documentation
- dbt provides a way to generate project documentation and render it as a website.
- Documentation includes:
  1. Information about the dbt project, models, and dependencies (DAG).
  2. Details on BigQuery warehouse schema, including column data types and table sizes.

Descriptions were added to models, columns, and sources for enhanced documentation. [Learn more about dbt documentation](https://docs.getdbt.com/docs/collaborate/documentation).

The **_stripe_schema.yml** file documents the models in the Stripe folder. An **_stripe.md** file contains doc blocks that describe fields (e.g., `order_status`). These blocks are referenced in the `stg_jaffle_shop__orders.yml` file.

The image below gives snapshots of documentations on the dim_customers data.

<img width="943" alt="dbt-docs" src="https://github.com/user-attachments/assets/aa4efc83-b49d-4a5b-98e8-b2328ae1ec5e">


## Deployment

1. **Deployment Environment**
   - A deployment environment called **Production Run** was created.
   - Connection to BigQuery was verified to ensure the correct warehouse target.

2. **Setting up Credentials**
   - Warehouse credentials were configured at the **Project Level** in dbt Cloud.

3. **Scheduling Jobs**
   - A job called **Daily Job** was scheduled to run at **8:00** and **16:00** UTC every day.
![Screenshot 2024-10-18 110211](https://github.com/user-attachments/assets/fb91bb83-fde4-45d5-bd1b-fcfc26947950)


## Query for Top 10 Customers by Lifetime Value

Here is an example query run on the `dim_customers` data to get the top 10 customers by lifetime value:

<img width="694" alt="result-query" src="https://github.com/user-attachments/assets/c64a51e3-d2b5-4123-8942-d51e3ab08032">

The tranformed tables, fct_orders and dim_customers can be imported into a BI tool to build reports for insights

## Conclusion
This project demonstrated how to transform sales data in BigQuery using dbt Cloud, while following best practices for data documentation, testing, and deployment.

---
lab:
  title: Use a SQL Warehouse in Azure Databricks
  description: You'll gain hands-on experience using SQL Warehouse to perform relational database operations on data lake files by creating custom database schemas and tables using standard SQL commands and CSV file uploads. You'll learn how to build interactive dashboards with SQL queries and bar chart visualizations that can be published and shared with business users for data exploration and reporting.
  duration: 30 minutes
  islab: true
  primarytopics:
    - AWS Databricks
---

# Use a SQL Warehouse in Azure Databricks

SQL is an industry-standard language for querying and manipulating data. Many data analysts perform data analytics by using SQL to query tables in a relational database. AWS Databricks includes SQL functionality that builds on Spark and Delta Lake technologies to provide a relational database layer over files in a data lake.

This exercise should take approximately **30** minutes to complete.

> **Note**: The AWS Databricks user interface is subject to continual improvement. The user interface may have changed since the instructions in this exercise were written.



## View and start a SQL Warehouse (You can skip this if you are able see the SQL Warehouse running)


1. In the **Overview** page for your AWS Databricks workspace, Ensure you are in the workspace - **pikapika**

    > **Tip**: As you use the Databricks Workspace portal, various tips and notifications may be displayed. Dismiss these and follow the instructions provided to complete the tasks in this exercise.

1. View the AWS Databricks workspace portal and note that the sidebar on the left side contains the names of the task categories.
1. In the sidebar, under **SQL**, select **SQL Warehouses**.
1. Observe that the workspace already includes a SQL Warehouse named **Starter Warehouse**.
1. In the **Actions** (**&#8285;**) menu for the SQL Warehouse, select **Edit**. Then set the **Cluster size** property to **2X-Small** and save your changes.
1. Use the **Start** button to start the SQL Warehouse (which may take a minute or two).


## Create a database schema

1. When your SQL Warehouse is *running*, select **SQL Editor** in the sidebar.
2. In the **Schema browser** pane, observe that the pikapika catalogue contains a database named **default**.
3. In the **New query** pane, enter the following SQL code:

    ```sql
   CREATE DATABASE retail_db_<your_name>;
    ```

4. Use the **&#9658;Run (1000)** button to run the SQL code.
5. When the code has been successfully executed, in the **Schema browser** pane, use the refresh button at the top of the pane to refresh the list. Then expand **pikapika** and **retail_db_<your_name>**, and observe that the database has been created, but contains no tables.

You can use the **default** database for your tables, but when building an analytical data store it's best to create custom databases for specific data.

## Create a table

1. Download the [`products.csv`](https://raw.githubusercontent.com/Kiran-255666/datasets/refs/heads/main/products.csv) file to your local computer, saving it as **products.csv**.
1. In the Azure Databricks workspace portal, in the sidebar, select **(+) New** and then select **Data**.
1. In the **Add data** page, select **Create or modify table** and upload the **products.csv** file you downloaded to your computer.
1. In the **Create or modify table from file upload** page, select the **retail_db_<your_name>** schema and set the table name to **products_<your_name>**. Then select **Create table** on the bottom right corner of the page.
1. When the table has been created, review its details.

The ability to create a table by importing data from a file makes it easy to populate a database. You can also use Spark SQL to create tables using code. The tables themselves are metadata definitions in the hive metastore, and the data they contain is stored in Delta format in Databricks File System (DBFS) storage.

## Create a dashboard

1. In the sidebar, select **(+) New** and then select **Dashboard**.
2. Select the New dashboard name and change it to `Retail Dashboard_<your_name>`.
3. In the **Data** tab, select **Create from SQL** and use the following query:

    ```sql
   SELECT ProductID, ProductName, Category
   FROM retail_db_<your_name>.products_<your_name>; 
    ```

4. Select **Run** and then rename the Untitled dataset to `Products and Categories_<you_name>`.
5. Select the **Canvas** tab and then select **Add a visualization**.
6. In the visualization editor, set the following properties:
    
    - **Dataset**: Products and Categories
    - **Visualization**: bar
    - **X axis**: COUNT(ProductID)
    - **Y axis**: Category

7. Select **Publish** to view the dashboard as users will see it.

Dashboards are a great way to share data tables and visualizations with business users. You can schedule the dashboards to be refreshed periodically, and emailed to subscribers.



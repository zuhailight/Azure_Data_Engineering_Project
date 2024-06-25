# Azure_Data_Engineering_Project

This project demonstrates an end-to-end Azure data engineering solution, starting from  On-premise SQL Server database ETL it into Power BI for Visualization and for Clien/User use. Lastly automated  Shedule Trigger Pipeline for this project.


A very special Thanks to Mr. K Talks Tech  for the project inspiration.

![azure diagram architecture drawio](https://github.com/zuhailight/Azure_Data_Engineering_Project/assets/102891795/e1922672-d439-46d2-8690-ef4b628ce2d7)

# Current Environment
- Utilized the AdventureWorks dataset from Microsoft.
- Set up an on-premises Microsoft SQL server on a personal computer.
- Imported the dataset using Microsoft SQL Server Management Studio.
- Created a new user profile, "zuhaili"
- Saved "zuhaili" profile's password credentials as a Secret in Azure Key Vault. 
 
![image](https://github.com/zuhailight/Azure_Data_Engineering_Project/assets/102891795/b293bfa0-e602-4ebe-9da3-c783300bf2d4)
![image](https://github.com/zuhailight/Azure_Data_Engineering_Project/assets/102891795/1594b8af-044e-4627-80d5-cb9d0b49b494)


# Data Ingestion (ADF Pipeline):

- Set up pipelines for ingesting data (Self-hosted Integration Runtime) from On-premises SQL Server Database using Azure Data Factory (ADF).
- In the ADF pipeline set a Lookup activity and ForEach to automated the process to find each tables in the database and then sink the tables to the RAW01 container in Azure Datalakes Gen 2 (ADLS Gen2) Storage account
- Where each table is format as Parquet format and have their own directory folder based on the table name inside the RAW01 container 



![pipeline adf](https://github.com/zuhailight/Azure_Data_Engineering_Project/assets/102891795/5b7f0240-036e-4ff2-9374-3e3c73c2eb03)


![image](https://github.com/zuhailight/Azure_Data_Engineering_Project/assets/102891795/d2d85658-7cbc-4879-8bb0-a4d5b120effc)

![image](https://github.com/zuhailight/Azure_Data_Engineering_Project/assets/102891795/0bc39590-c52b-49d0-82ed-286b9d97b557)


#  Data Cleaning & Transformation by (Databricks):
Using Databricks Notebooks:

 - Mount Azure Data Lake Gen2 to DBFS using credential passthrough
 - Change all the column name to a proper name
 -  Clean all the date data to daydate format DD/MM/YYYY
 -  Output to transform01 folder where each table is format as Delta format (for log/history) and they have their own directory folder based on the table name same as the RAW01 container.
 

 

https://github.com/zuhailight/Azure_Data_Engineering_Project/assets/102891795/eca22d40-ee74-4d01-9174-c04c1463f547

![image](https://github.com/zuhailight/Azure_Data_Engineering_Project/assets/102891795/571f25ee-6c12-498a-b1ba-1fc4e7d4ade2)
![image](https://github.com/zuhailight/Azure_Data_Engineering_Project/assets/102891795/d7e09bf0-e83c-46b3-aafc-05bd008c495c)
![image](https://github.com/zuhailight/Azure_Data_Engineering_Project/assets/102891795/b6003a74-50e6-4005-a889-a7cc0dd98135)





# Transformation Request by Client/User (Databricks):
Using Databrick Notebooks:

- Knowing how many null values per column on a table
- Rank the total sales per product (Join table and Rank transformation)
- Load the processed data from the TRANSFORM container into CLIENT container in ADLS Gen2.
  


https://github.com/zuhailight/Azure_Data_Engineering_Project/assets/102891795/70055ad4-c9b4-4c3c-9ebf-8dd74ccf216d


https://github.com/zuhailight/Azure_Data_Engineering_Project/assets/102891795/2a4e4069-2898-4176-bf7b-4ad64c150196

![image](https://github.com/zuhailight/Azure_Data_Engineering_Project/assets/102891795/eba73a72-8b21-4588-b980-bd47ba80f058)

# Loading to Data Warehouse (Azure Synapse Analytics):
- Linked  data with ADLS Gen2  
- Develop SQL scripts to Load data to Azure Synapse Analytics Data Warehouse SQL database (workspace)
- using Serverless SQL pool to run  Pipeline (Get Metada, ForEach & Stored Procedure activities from the SQL scripts)  to create Views in SQL database (Workspace)
  
![image](https://github.com/zuhailight/Azure_Data_Engineering_Project/assets/102891795/1d28fa0e-c462-4fa2-b601-b34cc162bdd2)

![image](https://github.com/zuhailight/Azure_Data_Engineering_Project/assets/102891795/b1e833c4-3f48-4e7b-80fc-9fa010eeeb0c)

# 5.	Reporting and Visualization (Power BI):

- Connect Power BI to Azure Synapse Analytics SQL Views to access the clean data for reporting.
- Develop interactive dashboards and reports in Power BI to visualize key metrics and insights.

![bi edit 2](https://github.com/zuhailight/Azure_Data_Engineering_Project/assets/102891795/3a2a480a-2ee5-4128-9cbb-569ee655631e)

# Security and data governance
- Use Key Vault Secret to securely save password
![image](https://github.com/zuhailight/Azure_Data_Engineering_Project/assets/102891795/86064ed3-ebfe-4e90-a8c2-fabb23833ab1)

  
- Use Mircosoft Entra ID (use to know as Azure Active Directory ) to set up Group and  add new user. (avoid to create new user and create  role assignments frequently)
![image](https://github.com/zuhailight/Azure_Data_Engineering_Project/assets/102891795/20f58480-5ea6-4450-af5d-ef9b5618d484)

# 7.	Run ADF PIPELINE to automated all this procedure with Trigger at specific time to update any changes in the SQL Server database.
- Implement data refresh Pipeline Schedules Triggers where any changes in the tables inside the database on SQL Server (for example, added new row) the Power Bi dashboard will be updated showing the current data
- The trigger will be set on each end of every month

  ![schedule Trigger setting](https://github.com/zuhailight/Azure_Data_Engineering_Project/assets/102891795/34f56b32-60ff-4c1a-a559-29c4efc31d45)

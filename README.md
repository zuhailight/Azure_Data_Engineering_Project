# Azure_Data_Engineering_Project

This project demonstrates an end-to-end Azure data engineering solution, starting from  On-premise SQL Server database ETL it into Power BI for Visualization and for Clien/User use. lastly automated  Shedule Trigger Pipeline for this project.


A very special Thanks to Mr. K Talks Tech  for the project inspiration.

![azure diagram architecture drawio](https://github.com/zuhailight/Azure_Data_Engineering_Project/assets/102891795/e1922672-d439-46d2-8690-ef4b628ce2d7)

# Current Environment
Utilized the AdventureWorks dataset from Microsoft. 
Set up an on-premises Microsoft SQL server on a personal computer. 
Imported the dataset using Microsoft SQL Server Management Studio. 
Created a new user profile, "zuhaili" 
Saved "zuhaili" profile's password credentials as a Secret in Azure Key Vault. 

![image](https://github.com/zuhailight/Azure_Data_Engineering_Project/assets/102891795/1594b8af-044e-4627-80d5-cb9d0b49b494)


# Data Ingestion (ADF Pipeline):

Set up pipelines for ingesting data (Self-hosted Integration Runtime) from On-premises SQL Server Database using Azure Data Factory (ADF). 
In the ADF pipeline set a Lookup activity and ForEach to automated the process to find each tables in the database and then sink the tables to the RAW01 container in Azure Datalakes Gen 2 (ADLS Gen2) Storage account 
Where each table have their own directory folder based on the table name inside the RAW01 container 

![pipeline adf](https://github.com/zuhailight/Azure_Data_Engineering_Project/assets/102891795/23912104-59d1-47a2-b995-f3ffab6c98a8)

![image](https://github.com/zuhailight/Azure_Data_Engineering_Project/assets/102891795/d2d85658-7cbc-4879-8bb0-a4d5b120effc)

![image](https://github.com/zuhailight/Azure_Data_Engineering_Project/assets/102891795/0bc39590-c52b-49d0-82ed-286b9d97b557)


#  Data Cleaning & Transformation by (Databricks):
Using Databricks Notebooks:

 - Mount Azure Data Lake Gen2 to DBFS using credential passthrough
 - Change all the column name to a proper name
 -  Clean all the date data to daydate format DD/MM/YYYY
 -  Output to transform01 folder 
 

 

https://github.com/zuhailight/Azure_Data_Engineering_Project/assets/102891795/eca22d40-ee74-4d01-9174-c04c1463f547


# 3.	Transformation Request by Client/User (Databricks):
Using Databrick Notebooks:

- Knowing how many null values per column on a table
- Rank the total sales per product (Join table and Rank transformation)

 Load the processed data from the TRANSFORM container into CLIENT container in ADLS Gen2.
  


https://github.com/zuhailight/Azure_Data_Engineering_Project/assets/102891795/70055ad4-c9b4-4c3c-9ebf-8dd74ccf216d


https://github.com/zuhailight/Azure_Data_Engineering_Project/assets/102891795/2a4e4069-2898-4176-bf7b-4ad64c150196




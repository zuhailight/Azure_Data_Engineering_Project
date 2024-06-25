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
In the ADF pipeline set a Lookup activity and ForEach to automated the process to find each tables in the database and then sink the tables to the RAW container in Azure Datalakes Gen 2 (ADLS Gen2) Storage account
Where each table have their own directory folder based on the table name inside the RAW container
![image](https://github.com/zuhailight/Azure_Data_Engineering_Project/assets/102891795/4ea60d87-e283-4c0e-93e1-34d4ef452f33)



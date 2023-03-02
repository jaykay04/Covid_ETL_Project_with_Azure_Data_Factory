# Covid_ETL_Project_with_Azure_Data_Factory
This Project is about Injesting couple of Covid-19 Dataset from the ECDC website, transforming it using various ADF components, then loading it into SQL Datawarehouse for the Analytics team to derive useful and actionable insights from these datasets.
We want to know the impact of Covid in the European Region as whole.

## Azure Data Factory
Azure Data Factory (ADF) is a fully managed, serverless data integration solution for ingesting, preparing, and transforming all your data at scale. It enables every organization in every industry to use it for a rich variety of use cases: data Engineering, migrating their on-premises SSIS packages to Azure, operational data integration, analytics, ingesting data into data warehouses, and more.

### Situation
We have various Covid-19 data form multiple sources. 
Due to the fact that these dataset are scattered everywher, it was became relatively difficult to extract useful information from them at a go.

### Task
The task of this project is to ingest the dataset from the various data sources, clean and transform the data to make it more robust and fit for purspose. 
The this cleaned data should then be loaded into a central repo, like Datawarehosue and Datalake so that the analytics team can consume it with their BI tools such as Power BI. Also, we can also run ML Models on Datalake.

### Approach
#### Environment SetUp
* Azure Subscroption
* Data Factory 
* Azure Blob Storage Account
* Data Lake Storage Gen 2
* Azure SQL Database
* Azure Databricks Cluster
* HD Insight Cluster
* Azure Devops

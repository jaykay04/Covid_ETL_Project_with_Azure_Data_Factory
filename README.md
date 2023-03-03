# Covid_ETL_Project_with_Azure_Data_Factory
This Project is about Injesting couple of Covid-19 Datasets from the ECDC website, transforming it using various ADF components, then loading it into SQL Datawarehouse for the Analytics team to derive useful and actionable insights from these datasets.
We want to know the impact of Covid in the European Region as whole during the year 2020.

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
#### Solution Architecture Diagram
<img src="https://github.com/jaykay04/Covid_ETL_Project_with_Azure_Data_Factory/blob/main/ADFProject%20Diagram.png">

#### Extraction/Ingestion
Four different datasets was ingested from both the ECDC website and azure blob storage into Datalake Gen2.
They are;
* Cases and Deaths Data
* Hospital Admissions Data
* Population Data
* Test Conducted Data

We used various components of **ADF Pipeline** activities to ingest the data from both HTTP Data Source and Azure Storage Account to Azure DataLake.
some of those activities are;
* Validation Activity
* Get Metadata Activity
* Copy Activity

#### Transformation
The Cases and Deaths data together with the Hospital admissions data was trasnformed using ADF Data flows.
The Data Flows transformation used on both dataset include;
* Select transformation
* LookUp transformation
* Filter Transfomration
* Join transformation
* Sort transformation
* Conditional split transofrmation
* Derived columns trannsformation
* Sink transformation et.c

These set of transformations was done to make the datasets more robust and fit for purpose.
<img src="https://github.com/jaykay04/Covid_ETL_Project_with_Azure_Data_Factory/blob/main/images/transform_hospital_admissions.png">
<img src="https://github.com/jaykay04/Covid_ETL_Project_with_Azure_Data_Factory/blob/main/images/tranform_cases_deaths.png">

For the Population data set, Azure databricks was solely used to transform it so that it can be robust and fit for purpose.
The following steps was taken to transform the data on Azure Databricks.
* Azure Datalake storage was mounted on databricks so as to allow databricks read the data into the pyspark notebook easily.
<img src="https://github.com/jaykay04/Covid_ETL_Project_with_Azure_Data_Factory/blob/main/images/mount_storage.png">

* Next the Population data was read and a temp view was created which was followed by pivoting the dataset by age group as shown below
<img src="https://github.com/jaykay04/Covid_ETL_Project_with_Azure_Data_Factory/blob/main/images/read_pivot_population_data.png">

* The LookUp data was read, followed by a Join transformation before the transformed data was written back to the mount point in ADLS
<img src="https://github.com/jaykay04/Covid_ETL_Project_with_Azure_Data_Factory/blob/main/images/join_tranformation_population%20data.png">

#### Load
Now that the datasets are now fully prepared, we loaded it into the SQL Datawarehouse for the Analytics team to consume with their BI tools with ease.
* The first thing was to create the tables in the SQL database that will house each of the datasets
<img src="https://github.com/jaykay04/Covid_ETL_Project_with_Azure_Data_Factory/blob/main/images/create_table_sql.png">
* After creating the tables, the copy activity was used to load the dataset to its respective tables in the SQL Datawarehouse.

### Result and Analysis
#### The SQL Datawarehouse was connected to Power BI for the following Insights and Visualizations
* Covid-19 Trend in the EU/EEA & UK 2020 by Cases, Deaths, Hospital Occupancy and ICU Occupancy
<img src="https://github.com/jaykay04/Covid_ETL_Project_with_Azure_Data_Factory/blob/main/images/Covid-19_trend_EU_Uk.png">

* Covid-19 Cases and Death breakdown by population in the UK, France and Germany
<img src="https://github.com/jaykay04/Covid_ETL_Project_with_Azure_Data_Factory/blob/main/images/Covid-19%20Trend%20for%20UK%2C%20Germany%20and%20France.png">

* Confirmed Cases Vs Total Deaths By Country
<img src="https://github.com/jaykay04/Covid_ETL_Project_with_Azure_Data_Factory/blob/main/images/Number%20of%20Cases%20Vs%20Deaths%20Per%20Country.png">

* Total Number of Covid test carried out Vs Confirmed Cases
<img src="https://github.com/jaykay04/Covid_ETL_Project_with_Azure_Data_Factory/blob/main/images/Covid%20test%20done%20per%20Country.png">

### Follow Me
* Linkedin: https://www.linkedin.com/in/joshua-gbegudu-6a7a59a9/
* Github: github.com/jaykay04
* Instagram: @Official_jaykay04

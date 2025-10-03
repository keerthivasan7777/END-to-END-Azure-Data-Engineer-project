# END-to-END-Azure-Data-Engineer-project
My Azure Data Engineer END to END Project

![Azure](https://img.shields.io/badge/Azure-0078D4?style=flat&logo=microsoft-azure)
![Databricks](https://img.shields.io/badge/Databricks-FF3621?style=flat&logo=databricks)
![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python)




# Azure End-to-End Data Engineering Project: Car Sales Analytics

## 🎯 Project Overview
This project demonstrates a complete data engineering pipeline on Azure Cloud, processing car sales data through a medallion architecture with incremental loading capabilities.

## 🏗️ Architecture


![Architecture Overview](image/architecture-diagram.jpg)
*High-level architecture of the data pipeline*

### 1. Resource Groups and Azure Resources

![Resource Groups](image/01-resource-groups.png)
*Azure Resource Groups containing all project resources*

![Resource Group Details](image/02-resource-group-details.png)
*Detailed view of resources in RG_Azure_Car_Project*

### 2. Azure Data Factory Pipelines

#### Source Preparation Pipeline
![Source Prep Pipeline](image/03-adf-source-prep-pipeline.png)
*source_prep pipeline - Initial data extraction from Git to Bronze layer*

#### Incremental Data Pipeline
![Incremental Pipeline](image/04-adf-incremental-pipeline.png)
*increm_data_pipeline - Watermark-based incremental loading*

### 3. Azure Data Lake Storage

#### Container Structure
![Storage Containers](image/05-storage-containers.png)
*ADLS containers: bronze, silver, gold, and unitymetastore*

#### Gold Layer Dimensional Model
![Gold Container Folders](image/06-gold-container-folders.png)
*Gold layer containing dimensional tables and fact table*

### 4. Azure SQL Database

#### Query Editor
![SQL Database Query](image/07-sql-database-query.png)
*SQL Database with water_table for watermark management*

#### Stored Procedure
![SQL Stored Procedure](image/08-sql-stored-procedure.png)
*UpdateWatermarktable stored procedure for incremental loading*

### 5. Azure Databricks Integration

#### Access Connector
![Access Connector](image/09-access-connector.png)
*Access Connector for Azure Databricks authentication*

#### Databricks Notebooks
![Databricks Notebooks](image/10-databricks-notebooks.png)
*Databricks notebooks for dimensional modeling and transformations*

### 6. Pipeline Execution Results

#### Job Run Details
![Job Run Details](image/11-databricks-job-run-details.png)
*Successful job execution with lineage information*

#### Job Run Graph
![Job Run Graph](image/12-databricks-job-run-graph.png)


### Data Flow
1. **Source Layer**: CSV files stored in Git repository
2. **Bronze Layer**: Raw data ingestion into Azure Data Lake Storage
3. **Silver Layer**: Cleaned and validated data
4. **Gold Layer**: Business-ready dimensional model
5. **Consumption**: Analytics-ready star schema

### Azure Services Used
- **Azure Data Factory**: Orchestration and ETL pipelines
- **Azure Data Lake Storage Gen2**: Data lake with hierarchical namespace
- **Azure Databricks**: Big data processing and transformation
- **Azure SQL Database**: Metadata and watermark management
- **Git**: Version control for datasets

## 📊 Data Model

### Dimension Tables
- `dim_branch`: Branch information
- `dim_date`: Date dimension
- `dim_dealer`: Dealer details
- `dim_model`: Car model information

### Fact Table
- `fact_sales`: Sales transactions

## 🔄 Pipeline Architecture

### 1. Source Preparation Pipeline (`source_prep`)
- **Purpose**: Initial data extraction from Git
- **Components**:
  - CopyGitData activity
  - Source dataset: `ds_git`
  - Sink: Azure Data Lake (Bronze container)

### 2. Incremental Data Pipeline (`increm_data_pipeline`)
- **Purpose**: Process only changed/new records
- **Components**:
  - Lookup activities (`last_load`, `current_load`)
  - Copy activity for incremental data
  - Stored procedure activity (`watermarkUpdate`)

## 🗂️ Storage Structure

## 💾 Database Components

### Azure SQL Database: `carsalessql`
- **Table**: `water_table` (tracking last processed records)
- **Stored Procedure**: `UpdateWatermarktable`
  - Input parameter: `@lastload varchar(2000)`
  - Purpose: Update watermark for incremental loading

## 📓 Databricks Notebooks

Located in workspace: `Databricks_notebooks/`
- `gold_dim_branch`
- `gold_dim_date`
- `gold_dim_dealer`
- `gold_dim_model`
- `gold_fact_sales`
- `DB_notebook`
- `silver_notebook`

## 🔐 Security & Access

- **Access Connector**: `carsacessconnector` for Azure Databricks
- **Resource Group**: `RG_Azure_Car_Project`
- **Location**: South India (primary), Central India (SQL)
- **Subscription**: Azure subscription 1

## 📈 Performance Metrics

- **Pipeline Execution Time**: ~1-2 minutes
- **Data Processing**: Successfully processed dimensional and fact tables
- **Job Status**: All tasks completed successfully

## 🚀 Key Features

1. **Incremental Loading**: Watermark-based approach to process only new/changed data
2. **Medallion Architecture**: Bronze → Silver → Gold layer progression
3. **Dimensional Modeling**: Star schema for analytics
4. **Version Control**: Git integration for pipeline configurations
5. **Scalability**: Cloud-native architecture supporting growing data volumes

## 📝 Prerequisites

- Azure Subscription
- Azure Data Factory
- Azure Data Lake Storage Gen2 account
- Azure Databricks workspace
- Azure SQL Database
- Git repository access

## 🛠️ Setup Instructions

1. Create resource group in Azure
2. Deploy Azure Data Lake Storage account
3. Set up Azure Data Factory
4. Configure Azure Databricks workspace
5. Create Azure SQL Database with watermark table
6. Deploy Access Connector for Databricks
7. Import notebooks into Databricks
8. Configure linked services in ADF
9. Deploy pipelines and datasets

## 📊 Monitoring

- Pipeline runs can be monitored through Azure Data Factory UI
- Databricks job runs visible in Jobs & Pipelines section
- SQL watermark table tracks processing timestamps

## 👤 Author

Keerthivasan R

## 📄 License

This project is for demonstration purposes.

![Logo](https://github.com/user-attachments/assets/055ef9ab-58d6-4d7a-8419-0c53365c6a73)  

[Matthew Walters LinkedIn](https://www.linkedin.com/in/matthew-walters-a66a4322)

# Introduction
On November 4, 2025, the Federal Reserve Bank of St. Louis (FRED) released the V2 of the FRED API.
[Announcement Link](https://news.research.stlouisfed.org/2025/11/fred-launches-new-version-of-api/)
FRED API V1 required each series to be called to retrieve observations. Version 2 allows for the bulk retrieval of series metadata and all observations for a release, greatly reducing the number of API calls and expanding the scope of data ingestion.

![Example Series Trend](https://mwalters-data-storage.atl1.cdn.digitaloceanspaces.com/Fabric_FRED_Data_Pipeline/Example_FRED_Report_Trend.png)

# Goal
The goal of this project is to call the FRED API V2 using a Microsoft Fabrice Notebook, ingest release data into a Fabric Lakehouse, then build a direct-lake semantic model from the lakehouse.

# Data Process
1. Date table is built in Spark Dataframe from year parameter.
2. API requests made to FRED, paging through responses.
3. API results are stored in Spark Dataframe.
4. Observations data is extracted from Spark Dataframe and semi-joined with Data table.
5. Series metadata is extracted from Spark Dataframe and semi-joined with Observations data.
6. Date, Observations, and Series tables are written to lakehouse in dbo schema.

# Steps for use:
1. Clone repo or download notebook and bim files.
2. Upload notebook to Fabric Workspace.
3. Open notebook and attach to lakehouse.
4. Update notebook parameters (API key, release ID, and # of years of data).
5. Run all cells of notebook.
6. From lakehouse, verify tables written from notebook, then create or update semantic model linked to lakehouse.
7. Using the ALM Toolkit, connect and update direct lake semantic model from previous step with the downloaded BIM file.
8. Create thin Power BI Report connected to the direct lake semantic model to visualize the data.

# Supplement
Workspace lineage after setup of the lakehouse, notebook, semantic model, and thin report:
![Workspace Lineage](https://mwalters-data-storage.atl1.cdn.digitaloceanspaces.com/Fabric_FRED_Data_Pipeline/Workspace_Lineage.png)


Example SQL Query to verify data:
![Example SQL Query](https://mwalters-data-storage.atl1.cdn.digitaloceanspaces.com/Fabric_FRED_Data_Pipeline/Example_SQL_Query.png)


Semantic Model Relationships after pushing changes from BIM file:
![Semantic Model Relationships](https://mwalters-data-storage.atl1.cdn.digitaloceanspaces.com/Fabric_FRED_Data_Pipeline/Semantic_Model_Relationships.png) 

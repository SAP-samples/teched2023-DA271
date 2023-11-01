# Exercise 0 - Getting Started - Preparing your system

**Section Goal:** Load all required data & models that are the base line for the following exercises.

We have prepared a simple data model to analyze product sales for a prototypical company. For this exercise we will simply load some basic sales tables and their data via replication from SAP HANA Cloud and add a minimal data model by importing a data model file (aka: ["CSN import"](https://help.sap.com/docs/SAP_DATASPHERE/c8a54ee704e94e15926551293243fd1d/23599e6347fb4c9e9a71c82f62449875.html)). This brings us quickly to the starting line of all subsequent exercises.

For better overview of the imported objects and their relationships & details, you'll also create an [entity-relationship model](https://help.sap.com/docs/SAP_DATASPHERE/c8a54ee704e94e15926551293243fd1d/a91c042549fb497384e756d5f5c71fde.html) and inspect the objects in the [impact & lineage analysis](https://help.sap.com/docs/SAP_DATASPHERE/c8a54ee704e94e15926551293243fd1d/9da4892cb0e4427ab80ad8d89e6676b8.html).

:warning: If you are not using an SAP academy system (TechEd 2023) or an SAP Guided Experience system (cp. [Exercise Requirements](../../README.md#prerequisites)), please jump to chapter **Steps in your own SAP Datasphere system** 

## Steps in SAP Academy systems and SAP Guided Experience Systems
If your system is an SAP Academy system (URL contains "academy") or an SAP Guided Experience system (URL contains "guided-experience-datasphere") the following steps are for you
### Use replication flow to import base tables of object model

-   Select the menu option **Data Builder** on the left-hand side
-   Select the option **New Replication Flow**

    ![](./images/launch_repl_flow_from_databuilder.png)

-   Create a new replication flow to import all relevant tables from source connection **HANA_CLOUD** and container **DSP1_OPENSAP** into target connection **SAP Datasphere**: 
    - Select source connection<br/>
    ![](./images/rf_select_source_connection.png)
    - select HANA_CLOUD as connection from which entities are to be replicated<br/>
    ![](./images/RF_source_selection.png)
    - select to import from source container **DSP1_OPENSAP**
    ![](./images/rf_select_source_container.png)<br/>
    ![](./images/select_container_dsp1_opensap.png)
    -select target connection **SAP Datasphere** <br/>
    ![](./images/select_target_conn.png)<br/>
    ![](./images/select_target_conn_datasphere.png)
    - launch selection of source objects to replicate<br/>
    ![](./images/select_source_objects.png)
-   Select the following 16 source objects:
    -   Addresses
    -   BusinessPartners - Business Partners
    -   Countries
    -   Employees
    -   HierarchyDirectory - Hierarchy Directory
    -   HierarchyDirectoryTexts - Hierarchy Directory Texts
    -   ProductCategories - Product Categories
    -   ProductCategoryTexts
    -   ProductHierarchy - ProductHierarchy
    -   ProductHierarchyNodes - Product Hierarchy Nodes
    -   ProductHierarchyNodesTexts - Product Hierarchy Nodes
    -   Products - Products
    -   ProductTexts
    -   Regions
    -   SalesOrderItems
    -   SalesOrder - Sales Orders <br/>
    ![](./images/object_selection.png)
    - Confirm the next dialog
    ![](./images/source_objects_screen2.png)
    - Your screen should now look like this <br/>
    ![](./images/rf_final_before_deploy.png)
-   Now choose **Deploy** button (top-left of screen) to save and render your replication flow ready to use. Save the flow as **RF_Initial_Load**
-   Once your RF is deployed, click the **Run** button (top-left of screen). This allows your local repository to house the source tables you imported from HANA Cloud. Once the run is finished, your final screen will look like this: <br/>
![](./images/repl_flow_final.png)

### Generate time data (only in SAP Guided Experience systems)
:warning: During SAP TechEd 2023, skip the step of generating time data. System setup scripts have taken care of it. Continue on to chapter *Import data model as CSN* below. 

If you are doing this exercise outside of SAP TechEd 2023 on an SAP Guided Experience system (i.e. the URL contains "guided-experience-datasphere"), you need to do the following steps
*   Launch Space Management
*   Go to section *Time Data* and click *Create Time Tables & Dimensions* 
![](./images/space_mgmt_create_time_data.png)
*   In the resulting popup, click *Create* 
![](./images/time_data_generation_popup.png)
*   Wait till the confirmation message "Time data created" appears
*   Leave *Space Management* and open *Data Builder*


### Import data model as CSN

-   Once replication flow’s run has completed, download the object model description (aka "CSN file") from Github [[link](../../model/DA271_DataModel%20-%20Quick%20Start.json)]
- Go back to the main screen of **Data Builder** and import the object model file via *+ > Import Objects from CSN/JSON file* <br/>
![](./images/import_from_landingpage.png)
-   You will be prompted to select the objects you want to import. Select the objects with the status of “Ready to Import” and click **Import CSN File**.
-   When prompted, if you want to reimport existing objects, choose to not reimport them, i.e. **Click No** 
-   Once those objects are imported, you’ll need to deploy them. Select all object that are not yet deployed and deploy them together
![](./images/deploy_from_databuilder.png) 

Now you have all the tables, their data and a minimal data model ready in the system. You should now start crafting your entity-relationship model. 

### Create entity-relationship model
-   On the **Data Builder** screen, select on the **E/R Models** tab, and click on the **New Entity – Relationship Model**
-   Within the **Repository** section (left panel), under **Views**, you will find the entities necessary to create your initial ER model.
-   Drag the **4VF_SalesOrderItems** entity onto the canvas
-   To add related entities, click on the entity and select the “**+**” sign. In the subsequent dialog choose to add all related entities and confirm. <br/>
![](./images/ER_builder.png)

-   Select all the related entities for **4VF_SalesOrderItems**; you will add the additional related entities using the same method until your ER looks like this <br/>
![](./images/small_er_diagram.png)

-   **Deploy** your model and name it **4EM_Overview_Simple**
-   To inspect all entities, select each one and inspect the View Properties panel on the right side of the screen. This gives details on their properties like semantic usage, columns, measures & attributes (only for 4VF_SalesOrderItems), semantic types as well as associations (also visible in the ER model itself). 
-   You can also preview the data of an entity by clicking on the entity and clicking on the **Preview Data** button on the top left after you selected a node on the canvas. 

- You can also view the impact & lineage graph of an entity by clicking on the **Impact and Lineage Analysis** button that exists on every node. Note that the subsequent popup makes a differentiation between data lineage and dependency lineage (cp. [SAP Help Documentation](https://help.sap.com/docs/SAP_DATASPHERE/c8a54ee704e94e15926551293243fd1d/9da4892cb0e4427ab80ad8d89e6676b8.html#loio9da4892cb0e4427ab80ad8d89e6676b8__section_dependency_analysis)).

## Steps in all other SAP Datasphere systems
:warning: During SAP TechEd 2023, the following chapter can be skipped. Continue down below with [Summary](#summary)

If your system is NOT an SAP academy system or an SAP Guided Experience system, you can still run all exercises as long as you have another SAP Datasphere system at your disposal. There are no requirements with regards to connected backends. 

:warning: [Exercise #4 - Currency Conversion](../ex4/) requires a connected SAP NetWeaver system that contains the required currency conversion tables. If you have no SAP NetWeaver system connected, you'll only be able to do all exercises *except for exercise #4*. 

Since the required HANA backend is not available to bring the respective data for our exercises, you'd need to load all data manually via CSV. Mid-term, we'll allow loading the data from SAP Data Marketplace.   

### Generate time data 
In this step, we generate a helper dimension containing time data and its properties. 

*   Launch Space Management
*   Go to section *Time Data* and click *Create Time Tables & Dimensions* 
![](./images/space_mgmt_create_time_data.png)
*   In the resulting popup, click *Create* 
![](./images/time_data_generation_popup.png)
*   Wait till the confirmation message "Time data created" appears
*   Leave *Space Management* and open *Data Builder*

### Import data model as CSN

-   Once replication flow’s run has completed, download the object model description (aka "CSN file") from Github [[link](../../model/DA271_DataModel%20-%20Quick%20Start.json)]
- Go back to the main screen of **Data Builder** and import the object model file via *+ > Import Objects from CSN/JSON file* <br/>
![](./images/import_from_landingpage.png)
-   You will be prompted to select which objects you want to import. Select all objects with the status of “Ready to Import” and click **Import CSN File**.
-   When prompted, if you want to reimport existing objects, choose to not reimport them, i.e. **Click No** 
-   Once those objects are imported, you’ll need to deploy them. Select all object that are not yet deployed and deploy them together
![](./images/deploy_from_databuilder.png) 

### Upload data into the tables
You'll need to upload data into all tables from CSV files. For SAP TechEd & Guided Experience, the respective data could be loaded from a connected SAP HANA Cloud system, but since your space has no connection to it, you'll need to provide the data manually

*   Download the [zip file containing all CSVs from Github](../../model/DA271%20-%20all%20CSVs.zip) 
*   Extract the zip file into some folder on your hard drive
*   In Data Builder, choose tab Tables. This will filter the objet list on the tables only
* For each and every table in the list (puh, yes, this is painful :frowning:), do the following steps
    *   Open table by clicking on its name in Data Builder
    *   Choose button Upload CSV in the menu bar <br/>
    ![](./images/table_upload_csv.png)
    *   In the prompt to "Import CSV File", find the file that has the same name as the table at hand <br/>
    ![](./images/import_csv_file_prompt.png)
    *   In the resulting dialog, all columns should automatically be matched and all you need to do is confirm with "Import". If for any reason you need to repeat the step and upload again, ensure to check "Delete Existing Data Before Upload" to avoid duplicate key errors <br/>
    ![](./images/import_csv_file_import_dialog.png)
*   Ensure that you have indeed upload data for all tables. If yes, the fun can now start :tada:

Now you have all the tables, their data and a minimal data model ready in the system. You should now start crafting your entity-relationship model. 

### Create entity-relationship model
-   On the **Data Builder** screen, select on the **E/R Models** tab, and click on the **New Entity – Relationship Model**
-   Within the **Repository** section (left panel), under **Views**, you will find the entities necessary to create your initial ER model.
-   Drag the **4VF_SalesOrderItems** entity onto the canvas
-   To add related entities, click on the entity and select the “**+**” sign. In the subsequent dialog choose to add all related entities and confirm. <br/>
![](./images/ER_builder.png)

-   Select all the related entities for **4VF_SalesOrderItems**; you will add the additional related entities using the same method until your ER looks like this <br/>
![](./images/small_er_diagram.png)

-   **Deploy** your model and name it **4EM_Overview_Simple**
-   To inspect all entities, select each one and inspect the View Properties panel on the right side of the screen. This gives details on their properties like semantic usage, columns, measures & attributes (only for 4VF_SalesOrderItems), semantic types as well as associations (also visible in the ER model itself). 
-   You can also preview the data of an entity by clicking on the entity and clicking on the **Preview Data** button on the top left after you selected a node on the canvas. 

- You can also view the impact & lineage graph of an entity by clicking on the **Impact and Lineage Analysis** button that exists on every node. Note that the subsequent popup makes a differentiation between data lineage and dependency lineage (cp. [SAP Help Documentation](https://help.sap.com/docs/SAP_DATASPHERE/c8a54ee704e94e15926551293243fd1d/9da4892cb0e4427ab80ad8d89e6676b8.html#loio9da4892cb0e4427ab80ad8d89e6676b8__section_dependency_analysis)).

## Summary

Now that you have your data and data model uploaded, we can continue with the core of session's exercises. 

Continue to - [Exercise 1 - Create Analytic Model](../ex1/)

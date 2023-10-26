# Exercise 0 - Getting Started - Preparing your system

**Section Goal:** Load all required data & models that are the base line for the following exercises.

We have prepared a simple data model to analyze product sales for a prototypical company. For this exercise we will simply load some basic sales tables and their data via replication from SAP HANA Cloud and add a minimal data model by importing a data model file (aka: ["CSN import"](https://help.sap.com/docs/SAP_DATASPHERE/c8a54ee704e94e15926551293243fd1d/23599e6347fb4c9e9a71c82f62449875.html)). This brings us quickly to the starting line of all subsequent exercises.

For better overview of the imported objects and their relationships & details, you'll also create an [entity-relationship model](https://help.sap.com/docs/SAP_DATASPHERE/c8a54ee704e94e15926551293243fd1d/a91c042549fb497384e756d5f5c71fde.html) and inspect the objects in the [impact & lineage analysis](https://help.sap.com/docs/SAP_DATASPHERE/c8a54ee704e94e15926551293243fd1d/9da4892cb0e4427ab80ad8d89e6676b8.html).

:warning: If you are not using an SAP academy system (TechEd 2023) or an SAP Guided Experience system (cp. [Exercise Requirements](../../README.md#prerequisites)), please jump to chapter **Steps in your own SAP Datasphere system** 

## Steps in SAP Academy systems and SAP Guided Experience Systems

-   Download CSN file from Github [[link](../../model/DA271_DataModel%20-%20Quick%20Start.json)]
-   Select the menu option **Data Builder** on the left-hand side
-   Select the option **New Replication Flow**

    ![](media/7cc0042d09475ab45aae465107ce8040.png)

-   Create a new replication flow to import all relevant tables from the **HANA Cloud** connection, **DSP1_OPENSAP** container (source connection) to **SAP Datasphere** (target connection)
<img width="740" alt="Screenshot 2023-10-23 at 3 34 01 PM" src="https://github.com/SAP-samples/teched2023-DA271/assets/144805208/da5d48f2-21db-41fd-8e9b-3780f6cab32a">
<img width="577" alt="Screenshot 2023-10-23 at 3 35 25 PM" src="https://github.com/SAP-samples/teched2023-DA271/assets/144805208/6b9322ea-be5a-4658-9c72-1ead5f0986cb">

   <img width="457" alt="Screenshot 2023-10-23 at 3 37 13 PM" src="https://github.com/SAP-samples/teched2023-DA271/assets/144805208/b3174689-70e3-45d1-aecb-666948a96d5a">
<img width="296" alt="Screenshot 2023-10-23 at 3 37 57 PM" src="https://github.com/SAP-samples/teched2023-DA271/assets/144805208/1b917931-23fc-4b26-9544-0fba72438bae">
<img width="578" alt="Screenshot 2023-10-23 at 3 38 57 PM" src="https://github.com/SAP-samples/teched2023-DA271/assets/144805208/1eea096b-6082-4464-bce0-a09f98b5bafb">
<img width="846" alt="Screenshot 2023-10-23 at 3 39 40 PM" src="https://github.com/SAP-samples/teched2023-DA271/assets/144805208/613ff26a-26c9-48e3-8f27-b2c6b039609b">
<img width="576" alt="Screenshot 2023-10-23 at 3 40 33 PM" src="https://github.com/SAP-samples/teched2023-DA271/assets/144805208/7b46584c-2a80-481f-bec5-d98d8a9fa2f0">

-   Select the following 16 source objects:
    -   Addresses
    -   BusinessPartners
    -   Countries
    -   Employees
    -   HierarchyDirectory
    -   HierarchyDirectoryTexts
    -   ProductCategories
    -   ProductCategoryTexts
    -   ProductHierarchy
    -   ProductHierarchyNodes
    -   ProductHierarchyNodesTexts
    -   Products
    -   ProductTexts
    -   Regions
    -   SalesOrderItems
    -   SalesOrder
-   Once the objects have been added, click the **Deploy** ![](media/491eeded4e8dac24fcb4fcc51eac0ac6.png) button (top-left of screen) to save and render your replication flow ready to use. Save the flow as **RF_Initial_Load**
-   Once your RF is deployed, click the **Run** ![](media/1b677828bdd6a3f8dca4be59e676d0d1.png)button (top-left of screen). This allows your local repository to house the source tables you imported from HANA Cloud.

    ![](media/f402d44cae5d77b15518700a78663801.png)

-   Once replication flow’s run has completed, import the CSN file that you downloaded in step #1 from the **Data Builder** screen

    ![](media/72759a4ef0978b980d4a5091b3641f26.png)

-   You will be prompted to select the objects you want to import. Select the objects with the status of “Ready to Import” and click **Import CSN File**.
-   When prompted, if you want to reimport existing objects, choose to not reimport them, i.e. **Click No** 
-   Once those objects are imported, you’ll need to deploy them. Select all object that are not yet deployed and deploy them together. 

    ![](media/097ca79424adc02a531fd2a677d5ac36.png)

-   Now you have all the tables, their data and a minimal data model ready in the system. You should now start crafting your entity-relationship model. On the **Data Builder** screen, select on the **E/R Models** tab, and click on the **New Entity – Relationship Model**
-   Within the **Repository** section (left panel), under **Views**, you will find the entities necessary to create your initial ER model.
-   Drag the **4VF_SalesOrderItems** entity onto the canvas
-   To add related entities, click on the entity and select the “**+**” sign. In the subsequent dialog choose to add all related entities and confirm. 

    ![](media/a4e14a98f18bdb880111743468f74797.png)

-   Select all the related entities for **4VF_SalesOrderItems**; you will add the additional related entities using the same method until your ER looks like this

    ![](media/942d19ab7c4219bf6c0597169cd14484.png)

-   **Deploy** your model and name it **4EM_Overview_Simple**
-   To inspect all entities, select each one and inspect the View Properties panel on the right side of the screen. This gives details on their properties like semantic usage, columns, measures & attributes (only for 4VF_SalesOrderItems), semantic types as well as associations (also visible in the ER model itself). You can also preview the data of an entity by clicking on the entity and clicking on the **Preview Data**![](media/4607e716afa73a5ce285b733d94c935d.png) button. 

- You can also view the impact & lineage graph of an entity by clicking on the **Impact and Lineage Analysis** ![](media/a727dcc612e497793134b01f08c97a17.png) button. Note that the subsequent popup makes a differentiation between data lineage and dependency lineage (cp. [SAP Help Documentation](https://help.sap.com/docs/SAP_DATASPHERE/c8a54ee704e94e15926551293243fd1d/9da4892cb0e4427ab80ad8d89e6676b8.html#loio9da4892cb0e4427ab80ad8d89e6676b8__section_dependency_analysis)).

## Steps in all other SAP Datasphere systems
You can 

## Summary

Now that you have your data and data model uploaded, we can continue with the core of session's exercises. 

Continue to - [Exercise 1 - Create Analytic Model](../ex1/)

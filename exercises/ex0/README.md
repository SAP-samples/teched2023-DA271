# Exercise 0 - Getting Started - Preparing your system

**Section Goal:** Load all required data & models that are the base line for the following exercises.

We have prepared a simple data model to analyze product sales for a typical company. For this exercise we will simply load this model with connections to the associated data from a CSN file so we can focus on the Analytic Model.

If you want to learn how to create data layer ER models like this, go here...

## Steps

-   Download CSN file from Github [[link](../../model/DA271_DataModel%20-%20Quick%20Start.json)]
-   Select the menu option **Data Builder** on the left-hand side
-   Select the option **New Replication Flow**

    ![](media/7cc0042d09475ab45aae465107ce8040.png)

-   Create a new replication flow to import all relevant tables from the **HANA Cloud** connection, **DSP1_OPENSAP** container (source connection) to **SAP Datasphere** (target connection)
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

-   Once replication flow’s run has completed, import the CSN file from the **Data Builder** screen

    ![](media/72759a4ef0978b980d4a5091b3641f26.png)

-   You will be prompted to select the objects you want to import. Select the objects with the status of “Ready to Import” and click **Import CSN File**.
-   Once those objects are imported, you’ll need to deploy them.

    ![](media/097ca79424adc02a531fd2a677d5ac36.png)

-   Now you have all the datasets needed to begin crafting your ER model. On the **Data Builder** screen, select on the **E/R Models** tab, and click on the **New Entity – Relationship Model**
-   Within the **Repository** section (left panel), under **Views**, you will find the entities necessary to create your initial ER model.
-   Drag the **4VF_SalesOrderItems** entity onto the canvas
-   To add related entities, click on the entity and select the “**+**” sign

    ![](media/a4e14a98f18bdb880111743468f74797.png)

-   Select all the related entities for **4VF_SalesOrderItems**; you will add the additional related entities using the same method until your ER looks like this

    ![](media/942d19ab7c4219bf6c0597169cd14484.png)

-   **Deploy** your model and name it **4EM_Overview_Simple**
-   Within the View Properties section, you can inspect the **attributes** and **measures** associated with a given entity. You can preview the data by clicking on the entity and clicking on the **Preview Data**![](media/4607e716afa73a5ce285b733d94c935d.png) button. You can also view the lineage of an entity by clicking on the **Impact and Lineage Analysis** ![](media/a727dcc612e497793134b01f08c97a17.png) button

## Summary

Now that you have your data and data model uploaded, we can continue to data modeling.

Continue to - [Exercise 1 - Create Analytic Model](../ex1/README.md)

# Getting Started - Preparing your system

**Section Goal:** Load all required data & models that are the base line for the following exercises.

We have prepared a simple data model to analyze product sales for a typical company. For this exercise we will simply load this model with connections to the associated data from a CSN file so we can focus on the Analytic Model.

If you want to learn how to create data layer ER models like this, go here...

## Steps

-   Download CSN from Github [[link](../../model/DA271_DataModel%20-%20Quick%20Start.json)]
-   Create new replication flow RF_Initial_Load to import all relevant tables from HANA Cloud connection DSP1_OPENSAP
-   Select the following 16 tables:
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
-   **Screenshot** Deploy & run the replication flow
-   Import CSN
-   Open ER Model
-   Now your initial ER should look like this **[Screenshot to upload]**
-   Inspect details in ER Model (contained objects, their inner workings)

## Summary

Now that you have your data and data model uploaded, we can continue to data modeling.

Continue to - [Exercise 1 - Create Analytic Model](../ex1/README.md)

# 

# Exercise 1: Build Analytic Model to prepare data consumption for end-user

**Goal**: In this step we prepare consumption of the imported data model via an Analytic Model. We start with a minimal model and subsequently enhance it step by step. On the way, we get to know the features of the Analytic Model editor including adding of dimensions, modelling of measures, preparation of variables and previewing data.

## Create Initial Analytic Model

We will now create an Analytic Model to support consumption of the imported data model.

User Steps:

-   Select the menu option **Data Builder** on the left-hand side
-   Under the **Analytic Model** tab\*\*,\*\* click on **New Analytic Model**
-   Because the system detects associated dimensions from our **4VF_SalesOrderItems**, you will see the screen below.
    -   **Enable** all measures and attributes, as well as the associated dimensions, and click **Import**

![](media/f7e27b3998798b8a4c9d74cd50059f96.png)

We start with this minimal model and subsequently enhance it step by step.

![](media/7d207fbeab53cbd8d37cec20fe28848e.png)

-   **Deploy** your model and name it **4AM_SalesOrderItems**
-   **Preview** the data

![](media/7fe2730f27132200b1e73c09a5563a64.png)

-   Check various dimensions to drill by, change their order, add a filter, etc
-   The **Builder** panel ![](media/acd718ea27982c9573ef49020840f9c1.png)is displayed at the right side of the application. You can show it or hide it by choosing **Query Builder Designer Panel**.
-   When you choose **Available Objects**, you get a list of all available dimensions and measures in the analytic model. Here you can select dimensions and measures and assign them directly to the table's rows or columns by clicking ![](media/7cdf02ef1f1fc62872287e4c403700da.png)Column or ![](media/8a01b48dd17bbbd968f3effdc7b8b319.png)Row.
-   Here, you can see the dimension PRODUCTID has been added a row. You also see the ability to drill-down into the PRODUCTID dimension. All the measures have been added as columns as well

![](media/aa14741a3acdada459f2d68f81927787.png)

-   You can filter on dimensions and measures using the ![](media/35c540e99672a162c9b1321d2ec4cd56.png) button (top-left area)
-   Click on **Model** to return to your analytic model

## Add Associated Dimensions

Add additional drill-dimensions by adding nested dimensions

User steps:

-   Select the **SALESORDERID** (**4VD_SalesOrders** dimension)
-   Within the Properties section, enable **PARTNERID, RESPONSIBLE & CREATION DATE** within the **Associated Dimensions** section
-   You should now see the added dimensions that stem from the **4VD_SalesOrders** dimension

![](media/516e49d65b42d31f120637a7d7254cb1.png)

-   We want to add the **4VD_Address** dimension, which is associated to the **4VD_BusinessPartners** dimension object
-   Your more robust analytic model should now look like this:

![](media/9b40e8559fdd329c5eff31f8f283f6b9.png)

-   Within the **Attributes** section of **Properties**, enable the following attributes for the given dimensions:
    -   Business Partner dimension: COMPANYNAME
    -   Address dimension: Country, REGION, CITY, STREET, POSTALCODE
-   Reopen data preview and confirm that you can now also drill by these dimensions (if, for any reason you do not see your added dimensions, **deploy** your Analytic Model first before continuing to preview data)

## Add Measures & Variables

Add calculated & restricted measures. In large organizations, its crucial to agree on common definition of KPIs. This is helpful for their reusability (saves time) and governance (we all use same definitions).

User steps:

-   To add a calculated measure, locate the **Measures** section within **Properties** and click the **+** sign. Select Calculated Measure

![](media/d21152bcc9058cac4fbc4a953bbd29b5.png)

-   Add calculated measure Average Price (AVG_PRICE) as GROSSAMOUNT / QUANTITY
-   Name your measure **Avg Price**

![](media/1550894b2d51f893439adbf52770ab3b.png)

-   You can navigate back to the main properties window by clicking on the object link, as shown below

![](media/2b01e176bee5cf7b7215a1b39fa127fe.png)

-   Following the previous navigation path, let’s now create **restricted measures**.
    -   Create **Domestic Gross Sales** based on source measure GROSSAMOUNT and with restriction as COUNTRY = 'DE' as an expression
    -   Create **International Gross Sales** based on source measure GROSSAMOUNT and with restriction as COUNTRY != 'DE' as an expression
-   Add a **Filter Variable** (within Properties Window) *YEAR* with the filter type of **Multiple single values**

![](media/2db949fc0c1dda668af857dffe3f4e2a.png)  
Many users will want to see only the current year. This way the system pre-filters on the current year. The same could be true for your own region.

-   **Deploy** your Analytic Model
-   Preview data and open the **Year** filter variable.

![](media/26f76cfa604c2ca94525b1730f6fda87.png)

-   Select years **2021, 2022, 2023** and click **OK**
-   Under **Dimensions,** drill into **Creation Date** and enable the row on **YEAR** to reveal the filtered years

![](media/e15014576b679911cbd8c14ff31bdd95.png)

## Introduce Model Enhancements

For preparation of subsequent exercises, we realize that we lack descriptions to products, companies, product categories and employees. We also realize that inherent hierarchies (managers have employees, regions have countries & cities, custom product groupings) are not contained.

User Steps:

-   Preview data
-   Drill by REGION and COUNTRY (as rows). Realize the need to understand their respective abbreviations
-   Drill by PARTNERID (as rows). Realize the need to also drill by COMPANYNAME to realize which customer this is
-   Drill by EMPLOYEEID. Realize you need to add Full Name into drill to realize which user this is. If you only drill by Full Name and two users had the same name, you'd not realize which individual this is. Also realize there is no way to know/see the organizational hierarchy
-   Drill by PRODUCTCATEGORY & PRODUCTID. Realize there are no product names or custom groupings of products (e.g. strategic products, low-end products or else)

## Summary

Note: One of the main goals in SAP Datasphere modelling is provide & leverage business semantics in datasets such that intelligent data consumers like SAP Analytics Cloud can leverage the same to simplify consumption, provide a rich end-user interaction.

Continue to - [Exercise 2 - Add Labels & Internationalization](../ex2/README.md)

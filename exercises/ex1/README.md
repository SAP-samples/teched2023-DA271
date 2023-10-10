# 

# Exercise 1: Build Analytic Model to prepare data consumption for end-user

**Goal**: In this step we prepare consumption of the imported data model via an Analytic Model. We start with a minimal model and subsequently enhance it step by step. On the way, we get to know the features of the Analytic Model editor including adding of dimensions, modelling of measures, preparation of variables and previewing data.

## Create Initial Analytic Model

We will now create an Analytic Model to support consumption of the imported data model.

We start with a minimal model and subsequently enhance it step by step. On the way, we get to know the features of the Analytic Model editor incl. adding of dimensions, modelling of measures, preparation of variables and previewing data.

## Add associated dimensions

Add additional drill-dimensions by adding nested dimensions

User steps:

-   Add dimensions for Business Partner & Address. Include attribute Company Name of Business Partner and Country, Region, City, Street, Postalcode of Address
-   Reopen data preview and confirm that you can now also drill by these dimensions

## Add Associated Dimensions

## Add Measures & Variables

Add calculated & restricted measures. (Note: Point out that in large organization its crucial to agree on common definition of KPIs. This is helpful for their reuse (saves time) and governance (we all use same definitions)

User steps:

-   Add calculated measure Average Price (AVG_PRICE) as GROSSAMOUNT / QUANTITY
-   Add restricted measures
    1.  Domestic Gross Sales (DOMESTIC_GROSSAMOUNT) based on measure GROSSAMOUNT and with restriction as COUNTRY = 'DE'
    2.  International Gross Sales (INTL_GROSSAMOUNT) based on measure GROSSAMOUNT and with restriction as COUNTRY != 'DE'
-   Add Filter Variable YEAR w settings multi-value, no default, not mandatory   
    Note: explain that many users will want to see only the current year. This way the system pre-filters on the current year. The same could be true for e.g. own region. Explain that other variable types exist also (w link to docu)
-   Save & deploy
-   Preview data and confirm empty prompt. Check new calculations (e.g. drill by country)
-   Redo prompt (button exists!) and filter on 2023. Confirm data is now filtered (e.g. by taking YEAR into drill-down)

## Add More Complex Measures & Variables

Showcase features count distinct & constant selection

User steps:

-   Add restricted measure All Countries (ALL_COUNTRIES_GROSSAMOUNT) based on measure GROSSAMOUNT and w empty expression. Activate constant selection on dimension COUNTRY  
    Note that constant selection ensures that a given dimension is taken out of drill-down even it actually is part of drill-down. This is important to compute reference figures (like e.g. here all countries). We could also have used a variable and used it in the restriction expression to make the list of reference countries configurable (optional exercise w/o guide)
-   Add calculated measure Share of Sales (SHARE_OF_SALES) w expression 100 \* GROSS_AMOUNT / ALL_COUNTRIES_GROSSAMOUNT
-   Add count distinct measure Customer Count (CUSTOMER_CNT) based on Dimension PARTNERID
-   Add calculated measure Avg Spend per Customer (AVG_GROSSAMOUNT_PER_CUSTOMER) w expression GROSSAMOUNT / CUSTOMER_CNT
-   **Deploy** entity
-   Preview data. Drill by COUNTRY and PARTNERID

## Introduce Model Enhancements

For preparation of subsequent exercises, we realize that we lack descriptions to products, companies, product categories and employees. We also realize that inherent hierarchies (managers have employees, regions have countries & cities, custom product groupings) are not contained. Also all amounts are in US Dollars, but this is neither shown nor converted into another currency.

User Steps:

-   Preview data
-   Drill by REGION and COUNTRY. Realize you need to understand their respective abbreviations to understand what you see on the screen.
-   Drill by PARTNERID. Realize You need to also drill by Company Name to realize which customer this is
-   Drill by Employee ID. Realize you need to add Full Name into drill to realize which user this is. If you only drilled by Full Name and two users had the same name, you'd not realize. Also realize there is no way to know/see the organizational hierarchy

Drill by Product Category & Product. Realize there are no product names or custom groupings of products (e.g. strategic products, low-end products or else)

## Summary

Note: One of the main goals in SAP Datasphere modelling is provide & leverage business semantics in datasets such that intelligent data consumers like SAP Analytics Cloud can leverage the same to simplify consumption, provide a rich end-user interaction.

Continue to - [Exercise 2 - Exercise 2 Description](../ex2/README.md)

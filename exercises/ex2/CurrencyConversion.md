# Currency Conversion

SAP Datasphere can perform currency conversion (aka: currency translation) fully aligned with the [respective functionality in SAP S/4](https://help.sap.com/docs/SAP_S4HANA_ON-PREMISE/8fbeed5f2046489696a50ac7fd76f9c6/d16ebe532789b44ce10000000a174cb4.html?locale=en-US) and SAP BW. The tables TCUR\* play a central role in the conversion since they contain the conversion rates, the list of supported currencies, conversion types and much more. These tables can be brought into SAP Datasphere in a very convenient fashion as described in [SAP Help " Enabling Currency Conversion with TCUR\* Tables and Views "](https://help.sap.com/docs/SAP_DATASPHERE/c8a54ee704e94e15926551293243fd1d/b462239ffb644d9baab4442a10a72edf.html). 

With a single click, the respective remote & local tables, the data flows to replicate data between them and convenience wrapper views can be imported into SAP Datasphere via any SAP ABAP connection. Subsequently, the HANA function [CONVERT_CURRENCY](https://help.sap.com/docs/HANA_SERVICE_CF/7c78579ce9b14a669c1f3295b0d8ca16/d22d746ed2951014bb7fb0114ffdaf96.html) does the automatic translation at runtime. For convenience, the SAP Datasphere modelling UIs simplify this by wrapping the currency conversion in easy-to-use modelling UIs.

Currency conversion can be executed both before and after aggregation:

-   with [currency conversion before aggregation](https://help.sap.com/docs/SAP_DATASPHERE/c8a54ee704e94e15926551293243fd1d/6e3d8bed7ece4c27ba10e2cc523915fe.html), the graphical view models a dedicated calculated column in which each row is converted individually. An Analytic Model consuming that view would normally aggregate all those converted values into one overarching figure

-   with [currency conversion after aggregation](https://help.sap.com/docs/SAP_DATASPHERE/c8a54ee704e94e15926551293243fd1d/ec00efb338f3421a87dab4006d7ce6c8.html), the Analytic Model offers a dedicated measure type "Currency Conversion Measure" that converts an already aggregated fact source measure. In this case, instead of converting each record individually and aggregating the converted values, first all records are aggregated and then the conversion happens on that final, aggregated figure. This is preferable both for performance and to minimize rounding errors.

In this exercise, we'll

-   get to know the currency semantics in modelling

-   Import currency conversion tables from SAP S/4 and replicate their contents

-   model a currency conversion measure

## Model currency semantics of fact source

So far, all amounts used in reporting, like GROSSAMOUNT and NETAMOUNT are just numbers without dedicated semantics. Since sales transactions often happen in different transaction currencies, it might not be valid to aggregate them without taking their transaction currency into account. Datasphere offers a dedicated semantic annotation to point out the relationship between a value (the amount) and its currency (the transaction currency used, when the amount was billed).

-   Open fact 4VF_SalesOrderItems
-   Preview its data
-   Confirm that each sales order item indeed has its transaction currency spelled out in column CURRENCY and its unit spelled out in column QUANTITYUNIT
-   Change semantic types of attributes

    -   set semantic type of CURRENCY to Currency Code
    -   set semantic type of QUANTITYUNIT to Unit of Measures

-   Change semantic type of measures

    -   set semantic type of NETAMOUNT to Amount w Currency and Unit Column to CURRENCY
    -   set semantic type of GROSSAMOUNT to Amount w Currency and Unit Column to CURRENCY
    -   set semantic type of TAXAMOUNT to Amount w Currency and Unit Column to CURRENCY
    -   set semantic type of QUANTITY to Quantity with Unit and Unit Column to QUANTITYUNIT
<img width="1127" alt="Screenshot 2023-10-10 at 2 09 18 PM" src="https://github.com/SAP-samples/teched2023-DA271/assets/144805208/11c07940-363f-465d-8886-f1bfa34a8865">

-   Save & Deploy

## Update Analytic Model and preview results

Refrest the Analytic Model to take note of the updated metadata. Then save and deploy.

-   Open *4AM_SalesOrderItems* and refresh page
-   Save & deploy
-   Open Data Preview

-   Confirm that all amounts now show a dollar sign. The quantity shows a unit symbol (EA for EACH) and the average price correctly denotes its unit as \$ / EA, i.e. dollars per piece.
<img width="1134" alt="Screenshot 2023-10-10 at 2 10 10 PM" src="https://github.com/SAP-samples/teched2023-DA271/assets/144805208/d5799b27-b20b-413f-b74b-4c05e3f8f62a">
-   

## Aggregation behavior for mixed currency data

The dollar sign semantics also affect the calculation to ensure currencies are calculated correctly. Let's manipulate the data and check how our actions influence the aggregation result. Since all data has been replicated into respective tables, we can manually change the data and understand the ripple effects of our changes.

-   Open table *SalesOrderItems*
-   Choose Data Editor
-   Change value of CURRENCY of the first record, i.e. sales order id 0050000001 and item id 0000000010 to EUR
-   Choose save

-   Refresh data preview of *4AM_SalesOrderItems*
-   Confirm that NETAMOUNT, GROSSAMOUNT, TAXAMOUNT and Avg Price now all show \* only, denoting that no value can be displayed  
    <img width="790" alt="Screenshot 2023-10-10 at 2 10 38 PM" src="https://github.com/SAP-samples/teched2023-DA271/assets/144805208/9357432f-3558-4d20-9c31-9e9b45c79709">


-   Drill by CURRENCY

-   Confirm that now all numbers display normally - the EUR amounts display a Euro sign (€) while the dollar amounts display a USD dollar sign (\$)  
    ![](5bb2d413a0eb1dee7d8ea442a845c8c5.png)  
    Since all currencies are now clean within each drill-row, aggregation is now correctly supported. Our changed row is displayed with its associated values for NETAMOUNT, GROSSAMOUNT and TAXAMOUNT as well as for its calculations (Avg Price)

-   Go back to the data editor of table *SalesOrderItems* to revert your change (i.e. change CURRENCY back from EUR to USD for the first record)
-   Save your change
-   Refresh the data preview of Analytic Model *4AM_SalesOrderItems*

## Load currency data from S/4 - Generate artfacts

Let's now replicate the currency conversion data from SAP S/4 into respective artefacts in SAP Datasphere. As described in the introduction, this has been packaged very conveniently.

-   Open Data Builder
-   Choose + \> Currency Conversion Views
-   Choose source S4_HANA

-   Open each of the for sections for Remote Tables, Data Flows, Tables & Views and inspect what objects will be created. You might want to read up [background in the documentation](https://help.sap.com/docs/SAP_DATASPHERE/c8a54ee704e94e15926551293243fd1d/b462239ffb644d9baab4442a10a72edf.html).

-   Confirm with CREATE  
    This will generate 32 objects, namely 8 remote tables, 8 data flows, 8 local tables and 8 views

-   Select all objects and deploy
-   Open table Exchange Rates (SAP.CURRENCY.TABLE.TCURR)
-   Preview the data to confirm it contains no data  
    We still need to run those 8 data flows to actually replicate the data from the remote tables (e.g. SAP.CURRENCY.RTABLE.TCURR) into the local tables. This is also required to ensure satisfactory performance during currency conversion

## Load currency data from S/4 - Run all data flows together via new task chain

We could now run all 8 data flows manually; just open each one and hit run. Since new exchange rate data will regularly be created in S/4, we'd rather have the system do this for us. We’ll prepare the regular replication via a new task flow that automatically executes all 8 data flows. We'll run it manually for our purposes, but we could also schedule it, for e.g. a daily cadence.

-   Create new task chain
-   Open repository section for data flows
-   Drag data flow "Conversion Factors (ODP)" onto the canvas and drop it on the drop zone

-   Choose <img width="38" alt="Screenshot 2023-10-10 at 2 11 14 PM" src="https://github.com/SAP-samples/teched2023-DA271/assets/144805208/749b5878-0aad-4d83-b6ac-a7209e173436">
sign on the node to add a parallel branch  
    <img width="545" alt="Screenshot 2023-10-10 at 2 11 43 PM" src="https://github.com/SAP-samples/teched2023-DA271/assets/144805208/ef313b5f-499a-488c-8984-a399fdf282fd">


-   Drag & drop data flow "Currency Code Names (ODP)" onto the new drop zone
-   
-   Repeat this 6 more times so that finally all 8 data flows are in parallel nodes of the same task flow  
    <img width="1078" alt="Screenshot 2023-10-10 at 2 12 13 PM" src="https://github.com/SAP-samples/teched2023-DA271/assets/144805208/bd65b73c-9d97-4285-bb42-0cdffa05215b">


-   Save & deploy as 4TC_TCUR_Replication

-   Open Data Integration Monitor and authorize system to run task chains 
<img width="1011" alt="Screenshot 2023-10-10 at 2 12 39 PM" src="https://github.com/SAP-samples/teched2023-DA271/assets/144805208/5a6875e8-c212-4465-b484-fdcd992a5883">

-   Change to Task Chain Monitor
-   Select entry 4TC_TCUR_Replication and choose Run
-   Choose to see run details of 4TC_TCUR_Replication
-   Refresh regularly until task chain has been executed. This should not take longer than 3-5 minutes
-   Once task chain is completed, reopen Data Builder for table Exchange Rates (SAP.CURRENCY.TABLE.TCURR)
-   Use data preview to confirm that table now contains data

## Create new currency conversion measure in Analytic Model and preview results

Now all groundwork has been laid for automatic currency conversion

-   Open *4AM_SalesOrderItems*
-   Choose to create a new measure of type Currency Conversion Measure
-   Fill its details as follows
<img width="350" alt="Screenshot 2023-10-10 at 2 13 07 PM" src="https://github.com/SAP-samples/teched2023-DA271/assets/144805208/303bc756-7377-4632-862a-f1b3eb4b344a">


-   Save & deploy

-   Preview data of Analytic Model

-   Confirm gross amount is now automatically converted and displayed as Gross Sales EUR  
<img width="801" alt="Screenshot 2023-10-10 at 2 13 55 PM" src="https://github.com/SAP-samples/teched2023-DA271/assets/144805208/0681e4b8-b5ce-41bc-a58a-025b6e7f255e">


# Add Labels & Internationalization

In this exercise we enhance the data model such that we add labels to countries & regions as well as full names to employees.

## Add Language-independent Labels to Employees & Companies

In this exercise we deal with language-independent labels for company names & employees. These obviously don't change with the user language.

### Update Employee Labels

-   Open entity V4D_Employees and do these changes
    -   Add semantic type of FULL NAME to Text
    -   Set Label Column of EMPLOYEEID to FULL NAME
-   Save & deploy

### Update Company Labels

-   Open entity V4D_BusinessPartners and do these changes
    -   Add semantic type of COMPANYNAME to Text
    -   Set Label Column of PARTNERID to COMPANYNAME
-   Save & deploy

### Update Analyic Model and Preview Results

The new metadata needs to be considered also by the Analytic Model. For it to take note of the updated metadata, the Analytic Model page needs to be loaded newly or refreshed. Subsequently you should save and deploy

-   Open *4AM_SalesOrderItems* and refresh page
-   Confirm that dimension PARTNERID now has a capital T (for Text) next to itself in the dimensin list
-   Confirm that RESPONSIBLE now also has a capital T next to itself in the dimension list
-   Save & deploy
-   Open Data Preview
-   Drill by PARTNERID and confirm that company name is now displayed
-   Drill by RESPONSIBLE and confirm that employee's full name is now displayed
-   Check drill-settings (three dots in dimension list on the right) and change presentation from ID+Description to Description or just to ID.

## Add Language-independent Labels For Products and Product Categories

Users feel a lot more at ease if they see data in their mother tongue rather than in some global language. To this end, SAP Datasphere provides the support of language-dependent labels. Depending on the data access language of the user (by default this is their logon language and mother tongue), the labels for objects are drawn in that specific language.

The recommended modelling setup for this to work is as follows:

An entity of usage type Dimension uses a text association to link itself to an entity of type Text. The association uses the dimensions key field (not some other field!) to link to the key of the Text entity. If the key is comprised of several key fields (also known as "composite key" or "compound key"), then this is totally fine. It is dedicatedly not recommended, and a warning will be issued in cases where:

-   the text association does not start from a dimension (but e.g. a Fact) or
-   the text association is on a non-key field of the dimension

Both cases are technically supported, but a warning will be issued. Both cases should rather have a dimension in the middle whose key is used in the text association. We'll see more of this below.

### Add Language-Specific Names to Product Dimension

-   Open entity ProductTexts and do these changes
    -   Change semantic usage to Text
    -   Set LANGUAGE to semantic type Language
    -   Set SHORT_DESCR to semantic type Text
    -   Set SHORT_DESCR as label column of PRODUCTID
-   Save & deploy
-   Add text association between 4VD_Product.PRODUCTID and ProductTexts
-   Save & deploy

As you see, here we follow the the standard way for language-dependent texts to work: a dimension (here 4VD_Products) with its key (here 4VD_Products .PRODUCTID) uses a text association to map to a text entity (here ProductTexts) and its key (here ProductTexts.PRODUCTID)

### Add Language-specific Names to Product Category

#### Create new Product Category Dimension

The product category so far is just an attribute of 4VD_Products. In order to comply w above-mentioned modelling best practices, we require a real product category dimension that subsequently links out to the Text entity for product category texts.

We'll therefore create a new dimension view for product categories and base it on the the imported table ProductCategories. We use the occasion to also hide fields that we don't want to expose to our analytics users (like CREATEDBY and CREATEDAT)

Since table ProductCategories only has three columns, the hiding of CREATEDBY and CREATEDAT leaves only a minimal dimension (consisting of just one field, PRODUCTCATEGORYID), but that's fine. In many more realistic cases there'd be own attributes to the category, like its category manager, a hierarchy on it or else, making it worthwhile to model this as a dimension in its own right.

-   Create new Graphical View
-   Draw table ProductCategories into the canvas
-   Add a projection node and choose to exclude columns CREATEDBY and CREATEDAT.
-   Choose final node and set semantic usage to Dimension
-   Save & deploy with name as *4VD_ProductCategories*

#### Update Product Category Text Entity

-   Open entity ProductCategoryTexts and do these changes
    -   Change semantic usage to Text
    -   Set LANGUAGE to semantic type Language
    -   Set SHORT_DESCR to semantic type Text
    -   Set SHORT_DESCR as label column of PRODUCTCATEGORYID
-   Save & deploy
-   Add text association between 4VD_ProductCategories.PRODUCTCATEGORYID and ProductCategoryTexts. PRODUCTCATEGORYID
-   Save & deploy
-   Add assocation between 4VD_Products and 4VD_ProductCategories

### Update ER Model

We should update the ER model w the new objects and their relationships in order to always have a good overview of our overarching model. This is easy to do since we can leverage the newly drawn associations to add the respective entities.

-   Open ER Model 4EM_Overview_Simple
-   Select node 4VD_Products and choose plus sign
-   Choose to add related entities 4VD_ProductCategories and ProductTexts
-   Save & deploy

### Update Analyic Model and Preview Results

The new metadata needs to be considered also by the Analytic Model. For it to take note of the updated metadata, the Analytic Model page needs to be loaded newly or refreshed. Subsequently you should save and deploy.

-   Open *4AM_SalesOrderItems* and refresh page
-   Confirm that dimension PRODUCTID now has a capital T (for Text) next to itself in the dimension list
-   Open node PRODUCTID and choose to add associated dimension PRODCATEGORYID. Note that it also has a capital T (for Text) next to itself
-   Save & deploy
-   Open Data Preview
-   Drill by PRODUCTID and confirm that Product Names are now being displayed
-   Drill by PRODCATEGORYID and confirm that the category ID name is now displayed
-   Change settings of your user. In section Language & Region, change data access language from English to French. Confirm with Close
-   Repeat drilling by PRODUCTID and PRODCATEGORYID. Confirm that you now see french texts for products and their category.

## Add Language-independent Labels For Countries, Regions

### Add Country Text

-   Open entity Countries and do these changes
    -   Add semantic usage to text
    -   Set LANGUAGE to semantic type Language
    -   Set COUNTRYTEXT to semantic type Text
    -   Set COUNTRYTEXT as label column of COUNTRYCODE
-   Save & deploy
-   Add assocation between 4VD_Addresses and its attribute COUNTRY and Countries.COUNTRYCODE
-   Save & deploy

Note the warning about key mapping in the properties of 4VD_Addresses. This is because of the above-mentioned modelling best practices. Here, the text association from 4VD_Address to the text entities for country text & region text are not using the key of 4VD_Addresses. For cleaner modelling, there should be an own Country dimension and an own Region dimension that are put in between like we did above for product categories.

![](media/64272377a7c415df34808e8cdce8a721.png)

### Add Region Text

-   Open entity Countries and do these changes
    -   Add semantic usage to text
    -   Set LANGUAGE to semantic type Language
    -   Set COUNTRYTEXT to semantic type Text
    -   Set COUNTRYTEXT as label column of COUNTRYCODE
-   Save & deploy
-   Add text assocation between 4VD_Addresses and its attribute REGION and REGION.REGIONCODE

### Update ER Model

We should update the ER model w the new objects and their relationships in order to always have a good overview of our overarching model. This is easy to do since we can leverage the newly drawn associations to add the respective entities.

-   Open ER Model 4EM_Overview_Simple
-   Select node 4VD_Addresses in the canvas and choose plus sign
-   Choose to add related text entities Countries & Regions
-   Save & deploy

### Update Analytic Model and Preview Results

The new metadata needs to be considered also by the Analytic Model. For it to take note of the updated metadata, the Analytic Model page needs to be loaded newly or refreshed. Subsequently you should save and deploy.

-   Open *4AM_SalesOrderItems* and refresh page
-   Confirm that dimension COUNTRY now has a capital T next to itself in the dimension list
-   Confirm that REGION now also has a capital T next to itself in the dimension list
-   Save & deploy
-   Open Data Preview
-   Drill by COUNTRY and confirm that country name is now displayed in French
-   Drill by REGION and confirm that region name is now displayed in French
-   Change data access settings of your user from French to English
-   Repeat drilling by COUNTRY and REGION and confirm that all their texts are now displayed in English again.

## Summary

Great work! You were able to enhance the data model by adding labels to countries & regions as well as full names to employees.

Continue to - [Exercise 4 – Currency](../ex4/README.md) Conversion

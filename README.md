[![REUSE status](https://api.reuse.software/badge/github.com/sap-samples/teched2023-DA271)](https://api.reuse.software/info/github.com/sap-samples/teched2023-DA271)


# DA271 - Delighting Analytics Users via Advanced Data Models in SAP Datasphere - Jump Start Session

## Session Summary

This repository contains the material for the SAP TechEd 2023 session :point_right: **DA271 - Delighting Analytics Users via Advanced Data Models in SAP Datasphere**.

Analyzing complex business data in the SAP Analytics Cloud solution is massively simplified if modelers prepare their data models well using the SAP Datasphere solution. They can prepare the relevant dimensions of analysis and company KPIs regardless of internal complexity, leverage hierarchies, automate currency conversion, and more. Dig deep into the modeling tools of SAP Datasphere, get hands-on experience modeling an end-to-end case, and quickly prepare analytics that delight business users. 

## Overview on what you'll learn

In this exercise we leverage the strong modelling capabilities of SAP Datasphere to add business semantics on data that have been ingested from remote sources. The goal is to prepare a flexible, rich, governed & understandable data model to our analytics users that they can subsequently use in their dashboards & data analysis. On the way, you'll get to know many of the modelling marvels that the SAP Datasphere team has added over the last year since TechEd 2022. 

Concretely, you'll get to know the following:

| **Area**                      | **Feature**                                                                                                                                                                                                                                                                                          |
|-------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| System setup                  |<ul><li>Replication flow for efficient and parallel onboarding of many source tables</li><li>CSN import for efficient, ad-hoc distribution of data models</li><li>Semantic basics around facts, dimensions, and associations</li><li>ER model for efficient object overview</li><li>Data lineage & dependency lineage of repository entities</li></ul>|
| Analytic model                | <ul><li>Dimension & attribute selection</li><li>Analytical data preview</li><li>Measure modelling for calculated measures, restricted measures, constant selection, count distinct & automatic currency conversion</li><li>Variable modelling for restricted measures & time-dependency</li></ul>|
| Labels & internationalization | <ul><li>Language-independent labels for attributes</li><li>Language-dependent labels via text entities that get associated to a dimension via a text association</li></ul>|
| Hierarchy modelling           | <ul><li>Level-based hierarchies</li><li>Classic parent-child hierarchies</li><li>Hierarchies with directories to get:<ul><li>data-driven hierarchy definition</li><li>support of text & dimension nodes</li><li>language-dependent labels for hierarchies and their nodes</li><li>time-dependent hierarchies</li></ul></li></ul>|
| Currency conversion           | <ul><li>Adding currency &amp; unit semantics to data layer artefacts</li><li>Import of currency conversion data from SAP S/4 into SAP Datasphere</li><li>Task chains for parallel execution of multiple data flows</li><li>Data integration monitor for inspection of task chain runs</li><li>Currency conversion measures in Analytic Model</li></ul>|

## Prerequisites

-   Google Chrome Browser
-   Access to [this GitHub repository](.)
-   Access to a suitable SAP Datasphere system
    - During TechEd 2023 hands-on sessions, you will be provided with user credentials for a personalized space in the [Datasphere system of the SAP Academy](https://academy.ap11.hcs.cloud.sap/dwaas-ui/index.html). 
    - Subsequent learners will be able to use the Guided Experience Systems for SAP Datasphere <br/> (request your user from [here](https://www.sap.com/products/technology-platform/datasphere.html) > "Experience SAP Datasphere")
    - Users can also use their own SAP Datasphere system to run through the exercises with minor adjustments. Since the system will not have the required backend systems available, the data import process will differ. [Preparatory exercise 0](./exercises/ex0/) offers a dedicated subchapter to cater to this.  
-   Object Model: Download the following model file to your computer: [DA271_DataModel - Quick Start.json](./model/DA271_DataModel%20-%20Quick%20Start.json) 
-   Time: 2+ hours 

## Exercises
-   [Overview on exercises & object model](./exercises/overview/)
-   [Exercise 0 - Getting Started - Uploading initial data and data model](exercises/ex0/)
-   [Exercise 1 - Build your Analytic Model to prepare data for consumption](exercises/ex1/)

:warning: If you are short on time, you can choose to only do one of the exercises [#2](./exercises/ex2/), [#3](./exercises/ex3/) and [#4](./exercises/ex4/), since they are all independent of each other. 

-   [Exercise 2 - Add labels and internationalization](exercises/ex2/)
-   [Exercise 3 - Add hierarchies](exercises/ex3/)
-   [Exercise 4 - Add currency conversion](exercises/ex4/)
-   [Session Wrap-Up](./exercises/Session%20Wrap-Up/)

## Code of Conduct

Please read the [SAP Open Source Code of Conduct](https://github.com/SAP-samples/.github/blob/main/CODE_OF_CONDUCT.md).

## How to obtain support

Support for the content in this repository is available during the actual time of the online session for which this content has been designed. Otherwise, you may request support via the [Issues](../../issues) tab.

## License

Copyright (c) 2023 SAP SE or an SAP affiliate company. All rights reserved. This project is licensed under the Apache Software License, version 2.0 except as noted otherwise in the [LICENSE](LICENSES/Apache-2.0.txt) file.

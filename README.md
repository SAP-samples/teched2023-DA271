![REUSE status](https://api.reuse.software/badge/github.com/SAP-samples/teched2023-DA271)

# DA271 - Delighting Analytics Users via Advanced Data Models in SAP Datasphere - Jump Start Session

## Description

This repository contains the material for the SAP TechEd 2023 session called :point_right: **DA271 - Delighting Analytics Users via Advanced Data Models in SAP Datasphere**.

This jump start session will give you the opportunity to build a scenario with exercises for SAP Datasphere. Analyzing complex business data in the SAP Analytics Cloud solution is massively simplified if modelers prepare their data models well using the SAP Datasphere solution. They can prepare the relevant dimensions of analysis and company KPIs regardless of internal complexity, leverage hierarchies, automate currency conversion, and more. Dig deep into the modeling tools of SAP Datasphere, get hands-on experience modeling an end-to-end case, and quickly prepare analytics that delight business users.

## Overview

In this exercise we leverage the strong modelling capabilities of SAP Datasphere to add business semantics on data that have been ingested from remote sources. The goal is to prepare a flexible, rich, governed & understandable data model to our analytics users that they can subsequently use in their dashboards & data analysis. On the way, you'll get to know many of the modelling marvels that the SAP Datasphere team has added over the last year since last TechEd. Concretely, you'll get to know the following:

| **Area**                      | **Feature**                                                                                                                                                                                                                                                                                          |
|-------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| System setup                  |<ul><li>Replication flow for efficient and parallel onboarding of many source tables</li><li>CSN import for efficient, ad-hoc distribution of data models</li><li>Semantic basics around facts, dimensions, and associations</li><li>ER model for efficient object overview</li><li>Data lineage & dependency lineage of repository entities</li></ul>|
| Analytic model                | <ul><li>Dimension & attribute selection</li><li>Analytical data preview</li><li>Measure modelling for calculated measures, restricted measures, constant selection, count distinct & automatic currency conversion</li><li>Variable modelling for restricted measures & time-dependency</li></ul>|
| Labels & internationalization | <ul><li>Language-independent labels to field</li><li>Language-dependent labels via own text entities that get associated to dimensions via text associations</li></ul>|
| Hierarchy modelling           | <ul><li>Level-based hierarchies</li><li>Classic parent-child hierarchies</li><li>Hierarchies with directories to get:<ul><li>data-driven hierarchy definition</li><li>support of text nodes</li><li>language-dependent labels for nodes &amp; hierarchies</li></ul></li></ul>|
| Currency conversion           | <ul><li>Adding currency &amp; unit semantics to data layer artefacts</li><li>Import of currency conversion data from SAP S/4 into SAP Datasphere</li><li>Task chains for parallel execution of multiple data flows</li><li>Data integration monitor for inspection of task chain runs</li><li>Currency conversion measures in Analytic Model</li></ul>|

## Requirements

-   Google Chrome Browser
-   Access to this GitHub repository
-   Access to SAP Datasphere system
-   You will also need the following .json file for these exercises: :point_right: [DA271_DataModel - Quick Start.json](DA271_DataModel%20-%20Quick%20Start.json)

>   :warning: **Once downloaded to your local machine, please unzip the file into a separate folder.** :warning: **You will need it for the exercises. So, please remember the file location of the unzipped file!**

## Exercises

Provide the exercise content here directly in README.md using [markdown](https://guides.github.com/features/mastering-markdown/) and linking to the specific exercise pages, below is an example.

-   [Getting Started - Uploading Initial Data and Data Model](exercises/ex0/)
-   [Exercise 1 - Build your Analytic Model to prepare data for consumption](exercises/ex1/)
    -   [Exercise 1.1 - Add associated dimensions](exercises/ex1/Add_Associated_Dimensions)
    -   [Exercise 1.2 - Add measures and variables](exercises/ex1/Add_measures_and_variables)
    -   [Exercise 1.3 - Add more complex measures and variables](exercises/ex1/Add_complex_measures_and_variables)
-   [Exercise 2 - Refine Data Layer entities to support consumption](exercises/ex2/)
    -   [Exercise 2.1 - Add labels and internationalization](exercises/ex2#exercise-21-sub-exercise-1-description)
    -   [Exercise 2.3 - Add Hierarchies](exercises/ex2#exercise-22-sub-exercise-2-description)
    -   [Exercise 2.3 - Add Currency Conversion](exercises/ex2/CurrencyConversion)
 
  [Summary](exercises/ex2/Summary)

**OR** Link to the Tutorial Navigator for example...

Start the exercises [here](https://developers.sap.com/tutorials/abap-environment-trial-onboarding.html).

**IMPORTANT**

Your repo must contain the .reuse and LICENSES folder and the License section below. DO NOT REMOVE the section or folders/files. Also, remove all unused template assets(images, folders, etc) from the exercises folder.

## Contributing

Please read the [CONTRIBUTING.md](./CONTRIBUTING.md) to understand the contribution guidelines.

## Code of Conduct

Please read the [SAP Open Source Code of Conduct](https://github.com/SAP-samples/.github/blob/main/CODE_OF_CONDUCT.md).

## How to obtain support

Support for the content in this repository is available during the actual time of the online session for which this content has been designed. Otherwise, you may request support via the [Issues](../../issues) tab.

## License

Copyright (c) 2023 SAP SE or an SAP affiliate company. All rights reserved. This project is licensed under the Apache Software License, version 2.0 except as noted otherwise in the [LICENSE](LICENSES/Apache-2.0.txt) file.

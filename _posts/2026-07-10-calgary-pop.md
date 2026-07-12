---
layout: single
classes: wide
title: "Calgary Population Viz: Part 1 - Sourcing & Cleaning Data"
date: 2026-07-10
author: "Aviva Rotstein"
tags: [Data Wrangling, OpenRefine, Data Normalization]

---

Option: Skip this exercise and go directly to [Part 2 - Data Visualization]({{ site.baseurl }}{% post_url 2026-07-11-calgary-pop %}). Clean data sets are provided.

> Problem Solving Objective: 
* Visualize Calgary's population growth by sector of the city over 50 years (1968-2019)

> Learning Objectives:
* Discover where to locate datasets
* Learn basic data cleaning and normalization skills with openRefine
* Understand importance of documenting any dataset modification - for replicability

### Step 1: Find datasets with licenses that allow for use
Where to start? 
* [Lunaris](https://www.lunaris.ca/), a discovery interface for data repositories across Canada
* [Calgary Open Data](https://data.calgary.ca/), portal with municipal datasets which have [Open Govenment License](https://data.calgary.ca/d/Open-Data-Terms/u45n-7awa). Note: Attribution statement is required by license for data use: "Contains information licensed under the Open Government Licence – City of Calgary"

Challenge: Search the listed sites and come up with appropriate data sets for the topic at hand. 
Suggested search terms: population, historical, sectors, communities (include 'calgary' if searching lunaris)

Data Chef's solution:
[Dataset 1: Community Sectors](https://data.calgary.ca/Base-Maps/Community-Sectors/mz2j-7eb5/about_data)
AND
[Dataset 2: Historical Calgary Community Populations](https://data.calgary.ca/Demographics/Historical-Calgary-Community-Populations/4mgk-hrwr)

(Both datasets found on Open Calgary)

### The overall plan
Take a look at the datasets. The variables in dataset 1 consist of:
 * Polygons for the sectors
 * Names of the sectors
 * Smaller Communities within those sectors. Note: Since multiple communities are listed in individual cells, separated by commas, this will require cleaning.
The other dataset includes a few variables that we aren't interested in. The important variables are year, population, and community. Note that there is no 'sector' variable, just the smaller communities within.
Data Chef's  overall idea is to create relationships between the datasets in Tableau. But first we need to do something about the multiple values in the first dataset.
Data Chef's plan is to 
    1. Duplicate the polygon/sector/communities dataset to transform the 1 dataset into 2 different tables - the first table will have the sector names and the community names. The community names will be separated using openRefine to put each community name on a different row or record. Data Chef will then pair each community name with the name of the sector to which it belongs. 
    2. The second table only requires us to delete the community name variable, leaving just the polygon and sector name variables.
We will then have 3 tables to work with
We also need to do a check making sure the community names and sector names are normalized across the tables, so that we can create relationships between tables eventually in Tableau in Part 2.

### Steps for data wrangling on OpenRefine
1. Download the datasets in csv format 
(Although they contain commas, OpenRefine is still capable of interpreting the data properly from the csv and Open Calgary has no tsv option. There is an xlsx option but it will cut off the polygon data.)
2. 




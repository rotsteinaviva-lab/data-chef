---
layout: single
classes: wide
title: "Calgary Population Viz: Part 1 - Sourcing & Cleaning Data"
date: 2026-07-10
author: "Aviva Rotstein"
tags: [Data Wrangling, OpenRefine, Data Normalization]

---

Simplified option: Skip this exercise and go directly to [Part 2 - Data Visualization]({{ site.baseurl }}{% post_url 2026-07-11-calgary-pop %}). Clean data sets will be provided.

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

Data Chef's chosen datasets:
* [Dataset 1: Community Sectors](https://data.calgary.ca/Base-Maps/Community-Sectors/mz2j-7eb5/about_data)
* [Dataset 2: Historical Calgary Community Populations](https://data.calgary.ca/Demographics/Historical-Calgary-Community-Populations/4mgk-hrwr)
(Both datasets found on Open Calgary)

### The overall plan
Take a look at the datasets. The variables in dataset 1 consist of:
 * Polygons for the sectors
 * Names of the sectors
 * Smaller Communities within those sectors
Data Chef's  overall idea is to create relationships between the datasets in Tableau. But first we need to do something about the multiple values in the first dataset.
The plan is to:
1. Duplicate the polygon/sector/communities dataset to transform the 1 dataset into 2 different tables - the first table will have the sector names and the community names. The community names will be separated using openRefine to put each community name on a different row or record. Data Chef will then pair each community name with the name of the sector to which it belongs. 
2. The second table only requires us to delete the community name variable, leaving just the polygon and sector name variables.
We will then have 3 tables to work with
We also need to do a check making sure the community names and sector names are normalized across the tables, so that we can create relationships between tables eventually in Tableau in Part 2.

### Steps for data wrangling on OpenRefine
1. Download the datasets in csv format 
(Although they contain commas, OpenRefine is still capable of interpreting the data properly from the csv and Open Calgary has no tsv option. There is an xlsx option but it will cut off the polygon data.)
2. Upload dataset one with sectors, community, polygon variables
3. Pick a variable and click the dropdown arrow -> edit cells -> common transformations -> Trim leading and trailing whitespace.
4. Repeat on all variables - shouldn't actually change anything in this case, but still good practice generally.
5. separate communities variable by comma: edit cells -> split multivalue cells (Split by using comma as separator)

6. Delete the polygon variable, (edit column -> remove this column) you can upload the spreadsheet again and create a separate project where you delete the communities variable so that we will have 2 spreadsheets - one with sectors and communities, and the other with sectors and polygons.
7. we want all the communities to have a corresponding sector, so let's edit cells-> fill down. now is clean, let's export
8. upload again - name it something else. edit column -> remove communities column
(we already know there's no whitespace to trim)
9. upload the historical data to openrefine
10. after trimming whitespace just to be sure,
cluster and edit - try different keying functions and methods and see what comes up, the only one that appears to need fixing is 
SCARBORO/ SUNALTA WEST vs SCARBORO/SUNALTA WEST. All the other compound entries (which are bad practice but we'll see what we can do) don't have spaces, so fix this one so no space, just /
11. add column based on this column, called normalized-name and add this code in the GREL Expression box to pull from the master-list
In the GREL Expression box, enter this  formula:
cell.cross("master-list", "Communities").cells["Communities"].value[0]
12. Replace master-list with the exact project name of your master file.
Replace Communities with the exact header name of the column in your master list.
Click OK. If a name matches your master list perfectly, the clean master name will instantly fill the new column. If it does not match, the cell will remain blank. Then we can isolate and fix the blanks
13. in the new normalized-name column drop down choose facet > customized facets > Facet by blank
There should be 130 blanks. click true
14. Now that we know which values we have to fix
15. duplicate the original column with names of communities and call it final-names
find and replace 
CHARLESWOOD/COLLINGWOOD with CHARLESWOOD and SCARBORO/SUNALTA WEST with SCARBORO
(the communities are in the same sector and because we're not using the community names in our visual, just to connect the datasets to each other, so this is fine). 
16. The remaining observations/rows in final-names which correspond with blanks in normalized-names are all residual wards. There are 14.

FOr this data-chef consulted AI
AI prompt:
assign the various residual wards in Calgary into the following sectors as closely as possible: north, east, centre, northwest, northeast, west, southeast, south

2nd prompt: ask AI to put the resideual wards in a table
Google AI cites wikipedia and says: If you isolate the Residual Wards (Residual Sub-Areas) specifically and map each one to the single geographic planning sector where its absolute majority of land mass sits, they organize neatly into the table below.

Because wards can occasionally straddle lines, this placement identifies the primary, dominant sector for each residual zone. I'm adding to the clean sector-community dataset IN excel SO IT LOOKS LIKE THIS: - screen capture

This is the info AI gave me based on wikipedia info

Residual Ward 1 > Northwest
Residual Ward 2 > Northwest
Residual Ward 3 > North
Residual Ward 4 > North
Residual Ward 5 > Northeast
Residual Ward 6 > West
Residual Ward 9 > Southeast
Residual Ward 10 > East
Residual Ward 12 > Southeast
Residual Ward 13 > South
Residual Ward 14 > South
Wards 7, 8, & 11 > Centre

Go back to the file with community and sector names add the 14 residual wards as community names to the sector-community dataset manually with their corresponding sector so that they are all accounted for, making sure to use the exact case and content of the historical spreadsheet.



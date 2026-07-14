---
layout: single
classes: wide
title: "Calgary Population Viz: Part 1 - Sourcing & Cleaning Data"
date: 2026-07-10
author: "Aviva Rotstein"
tags: [Data Wrangling, OpenRefine, Data Normalization]

---

Simplified option: Skip this exercise and go directly to [Part 2 - Data Visualization]({{ site.baseurl }}{% post_url 2026-07-11-calgary-pop %}). Clean data sets will be provided.

# Project Overview

## Objectives
*   **Problem:** Visualize Calgary's 50-year population growth (1968-2019) by city sector.
*   **Learning:** Find datasets, clean data with OpenRefine, and document changes for replicability.

## Data Sources
*   **Platform:** [Calgary Open Data](https://data.calgary.ca) ([Open Government Licence](https://data.calgary.ca/d/Open-Data-Terms/u45n-7awa)).
*   **Required Attribution:** *"Contains information licensed under the Open Government Licence - City of Calgary"*
*   **Selected Datasets:**
    *   [Dataset 1: Community Sectors](https://data.calgary.ca/Base-Maps/Community-Sectors/mz2j-7eb5/about_data) (Sectors, Communities, Polygons)
    *   [Dataset 2: Historical Calgary Community Populations](https://data.calgary.ca/Demographics/Historical-Calgary-Community-Populations/4mgk-hrwr) (Relevant variables: Years, Population, Communities)

## Target Architecture
Transform the data into three normalized tables to build relationships in Tableau:
1.  **Table 1 (Sector-Community):** Sector names paired with individual community names.
2.  **Table 2 (Sector-Polygon):** Sector names paired with spatial polygon data.
3.  **Table 3 (Population Data):** Historical population data with normalized community names.

> 🧠 **Licensing & Ethics Reflection:** *Data is a shared public resource, but it comes with strings attached. What are the ethical implications of using civic data without giving proper credit? How does compliance with the Open Government Licence protect your academic credibility and support "open data"?*

***

# Data Wrangling Instructions

## Phase 1: Prepare Tables 1 & 2 (Sectors & Communities)

1.  **Download:** Get Dataset 1 in CSV format.
    > 🧠 **Technical Reflection:** *Open Calgary offers XLSX formats, but we are choosing CSV. Why are we avoiding XLSX here, i.e., what risk might it pose to long text fields like spatial/polygon data?*
2.  **Import:** Create a new project in OpenRefine with this file. Download open source data tool OpenRefine [here](https://openrefine.org/).
3.  **Trim:** Click column dropdowns → **Edit cells** → **Common transformations** → **Trim leading and trailing whitespace** (Apply to all columns).
    > 🧠 **Data Cleanliness Reflection:** *Invisible spaces look identical to humans but are completely different strings to a computer. What would happen in Tableau if "Northwest" and "Northwest " tried to link?*
4.  **Split:** On the communities column, click **Edit cells** → **Split multi-value cells** (Use a comma as the separator).
5.  **Fill:** On the sector column, click **Edit cells** → **Fill down** to fill newly created rows.
    > 🧠 **Data Structure Reflection:** *Why is the "Fill Down" step critical immediately after splitting multi-value cells? What happens to the structural integrity of our records if we skip it?*
6.  **Create Table 1:** Delete the polygon column (**Edit column** → **Remove this column**). Export as CSV (e.g., `clean-data-sector-community.csv`).
7.  **Create Table 2:** Re-import the original CSV into a separate project. Delete the communities column (**Edit column** → **Remove this column**).
8.  **Export** as TSV (tab-separated values, e.g., `clean-polygon-data.tsv`).

## Phase 2: Clean and Normalize Table 3 (Population - Historical)

1.  **Import:** Upload the historical population dataset to OpenRefine.
2.  **Trim:** Run the whitespace trim transformation on all columns.
3.  **Cluster:** Click the community name dropdown → **Edit cells** → **Cluster and edit**. 
4.  **Fix Typos:** Merge `SCARBORO/ SUNALTA WEST` into `SCARBORO/SUNALTA WEST` (remove the space after the slash).
5.  **Cross-Reference:** Create a new column named `normalized-name` using this GREL formula to check against your master file:
    ```grel
    cell.cross("clean-data-sector-community", "Communities").cells["Communities"].value
    ```
    > 🧠 **Automation & Replicability Reflection:** *Instead of visually scanning thousands of rows for mismatches, we are using a relational lookup (`cell.cross`). How does this approach reduce human error and guarantee that another researcher can replicate your cleaning process exactly?*
6.  **Filter Blanks:** Click the `normalized-name` dropdown → **Facet** → **Customized facets** → **Facet by blank**. Click **True** to isolate the 130 unmatched rows.
7.  **Standardize Compounds:** Duplicate the original community name column, name it `final-names`, and execute find-and-replace transformations:
    *   Change `CHARLESWOOD/COLLINGWOOD` to `CHARLESWOOD`
    *   Change `SCARBORO/SUNALTA WEST` to `SCARBORO`
    > 🧠 **Data Integrity Reflection:** *We are deliberately flattening compound community names (like changing "CHARLESWOOD/COLLINGWOOD" to "CHARLESWOOD") because our final visual is at the sector level, not the community level. Why is it acceptable to lose granular community precision in this specific project? When would this compromise be considered bad practice?*
8.  **Drop Temporary Columns:** Delete the temporary `normalized-name` column (the one containing the 130 blanks). Keep the `final-names` column, as it now holds your corrected and standardized values for the final visualization.
9.  **Export** as TSV (tab-separated values, e.g., `clean-historical-data.tsv`).
 

## Phase 3: Map Residual Wards

1.  **Identify:** The remaining 14 unmatched rows represent residual wards.
2.  **Reference:** Use the geographic mapping table below to assign these wards to the most accurate sector overlap possible. [This map](https://www.calgary.ca/council/mayor/wardmap.html) from the City of Calgary consulted to produce the table below.

| Ward Zone | Assigned Sector |
| :--- | :--- |
| Residual Ward 1, 2 , 4| Northwest |
| Residual Ward 3 | North |
| Residual Ward 5, 10 | Northeast |
| Residual Ward 6 | West |
| Residual Ward 7, 8 | Centre |
| Residual Ward 9 | East |
| Residual Ward 11, 13, 14 | South |
| Residual Ward 12 | Southeast |


3.  **Update Master:** Open your `clean-data-sector-community.csv` file in Excel.
4.  **Append:** Manually add these 14 Residual Wards as communities alongside their assigned sectors. Match the exact casing used in the historical population file.

  > 🧠 **Data Replication Reflection:** *In Step 4, we transitioned from OpenRefine to manual editing in Excel to append the final 14 rows. What documentation must you keep to ensure that a third party can perfectly duplicate this hybrid workflow? How does a strict "change log" prevent a dataset from becoming a black box?*

***

## Your datasets are now fully cleaned, normalized, and ready for Tableau in [Part 2]({{ site.baseurl }}{% post_url 2026-07-11-calgary-pop %}).

***

## References 
(Includes [Part 2]({{ site.baseurl }}{% post_url 2026-07-11-calgary-pop %}) References)

City of Calgary. (2026, May 19). Community Sectors [Data set]. Open Calgary. [https://data.calgary.ca/Base-Maps/Community-Sectors/mz2j-7eb5/about_data](https://data.calgary.ca/Base-Maps/Community-Sectors/mz2j-7eb5/about_data)

City of Calgary. (2026, May 6). Historical community populations [Data set]. Open Calgary. [https://data.calgary.ca/Demographics/Historical-Calgary-Community-Populations/4mgk-hrwr](https://data.calgary.ca/Demographics/Historical-Calgary-Community-Populations/4mgk-hrwr)

City of Calgary. (2026). Ward and community map. [https://www.calgary.ca/council/mayor/wardmap.html](https://www.calgary.ca/council/mayor/wardmap.html)

## Software 
(Includes [Part 2]({{ site.baseurl }}{% post_url 2026-07-11-calgary-pop %}) Software)

OpenRefine. (2026). OpenRefine (Version 3.10.0) [Computer software]. [https://openrefine.org/](https://openrefine.org/)

Microsoft Corporation. (2026). Microsoft Excel 365 [Computer software]. [https://microsoft.com](https://microsoft.com)

Tableau Software. (2025). Tableau Desktop (Version 2025.1.2) [Computer software]. [https://tableau.com](https://tableau.com)


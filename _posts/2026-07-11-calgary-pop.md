---
layout: single
classes: wide
title: "Calgary Population Viz: Part 2 - Visualization"
date: 2026-07-11
author: "Aviva Rotstein"
tags: [Tableau, Data Viz]

---

## Phase 4: Building the Visualization in Tableau
Note: Phases 1-3 can be found in [Part 1]({{ site.baseurl }}{% post_url 2026-07-10-calgary-pop %})

[Download the Sector-Community Data (CSV)]({{ './data/clean-data-sector-community.csv' | relative_url }})<br>
[Download the Polygon Data (TSV)]({{ './data/clean-polygon-data.tsv' | relative_url }})<br>
[Download the Historical Data (TSV)]({{ './data/clean-historical-data.tsv' | relative_url }})

## Step 1: Initialize Tableau and Connect the Spatial Data
1. Open **Tableau Desktop** (accessible via your free academic license).
2. In the left-hand pane under **Connect**, click **To a File** → **More...**
3. Navigate to and select your spatial file: `clean-polygon-data.tsv`.
4. Locate the data type icon (currently showing **Abc**) above your polygon field. Click it and change the data type from **String** to **Spatial**.
5. Switch to **Sheet 1** at the bottom of the screen. Drag your spatial `polygon` field directly into the centre of the canvas to verify that the map of Calgary's sectors renders correctly.

> 🧠 **Tableau Architecture Reflection:** *Why must we set the data type to "Spatial" instead of leaving it as a "String"? How does it alter how the canvas treats the coordinates?*

***

## Step 2: Establish Logical Relationships (The Noodle Model)
1. Click the **Data Source** tab in the bottom-left corner to return to your data canvas.
2. Next to *Connections*, click **Add** to bring in your second dataset. Select and drag `clean-data-sector-community.csv` onto the canvas. Tableau should automatically detect and create a relationship line ("noodle") linking the two tables via the `Sector` field.
3. Click **Add** again to connect your final dataset: `clean-historical-data.tsv`. Drag it onto the data canvas.
4. Because the field names differ, Tableau will prompt you to define the relationship manually. Under the relationship settings, map the fields together by setting:<br>
`Communities (from clean-data-community-sector.csv) = Final-Names (from clean-historical-data.tsv`
5. Verify the data types for this historical table:
   * Click the data type icon above `Population` and ensure it is set to **Number (Whole)**.
   * Click the data type icon above `Years` and change it to **Date**. 

> 🧠 **Data Modeling Reflection:** *We are linking three separate files using Tableau's logical relationship layer rather than hard-joining them into a single flat table. How does keeping these tables distinct protect our computer's memory when processing a larger dataset? What might happen to our polygon data rows if we performed a standard flat physical join?*

***

## Step 3: Configure the Canvas and Interactive Filters
1. Go back to your worksheet (**Sheet 1**) and double-click the sheet tab at the bottom to rename it: `Calgary's Population by Sector (1968-2019)`.
2. Drag the `Population` measure from the left sidebar and drop it onto the **Label** card. Tableau will initially display a massive number representing the aggregated sum of all 50 years combined.
3. To slice this data over time, drag the `Years` field into the **Filters** shelf.
4. In the pop-up dialog box, select **Years**, click **Next**, check the box for **All** to include the full timeline, and click **Apply** then **OK**.
5. Right-click or click the dropdown arrow on the `Years` pill now sitting inside your Filters shelf, and select **Show Filter**. The filter control will appear on the right side of your screen.
6. Click the dropdown arrow at the top right of this new interactive filter card and change its display style to **Single Value (Slider)**. Slide it back and forth to see the total population text dynamically update year by year.

***

## Step 4: Map the Sectors and Adjust Label Visibility
1. Drag the `Sector` dimension from your `clean-data-sector-community.csv` file and drop it directly onto the **Label** card. You will now see individual population numbers broken down by city sector.
2. If some sector labels are hidden or missing due to space constraints, click the **Label** icon card on the Marks shelf.
3. Check the box that says **Allow labels to overlap other marks**. 
4. To add a visual narrative to the data density, drag the `Population` measure from your sidebar a second time, but drop it directly onto the **Color** card.

***

## Step 5: Format the Typography, Tooltips, and Legends
1. **Reposition Labels:** Click directly on any sector label on your map canvas and drag it manually to fine-tune its placement.
2. **Format Text:** Click the **Label** icon card, click the font dropdown, and change the typography to **Tableau Semibold** for better map legibility.
3. **Clean Tooltips:** Click the **Tooltip** card on the Marks shelf. In the text editor window, delete any messy file paths or source system prefixes attached to the sector variable names.
4. **Rename Legends:** Click the dropdown menu at the top of your year filter card and your color legend card, select **Edit Title**, and simplify their titles to `Year` and `Population` respectively.
5. **Restrict Filter Scope:** Click the dropdown menu on your `Year` slider control, navigate to **Customize**, and uncheck **Show "All" Value**. 

> 🧠 **User Experience (UX) Reflection:** *Why is it an important design choice to hide the "All" option on a historical timeline slider? What visual misinterpretations occur if an end-user accidentally selects "All" when viewing a geographic population density map over a 50-year span?*

***

## Step 6: Create a Data Extract and Publish to Tableau Public
1. Click the **Data Source** tab in the bottom-left corner one last time.
2. In the top-right corner of the data screen, change the Connection setting from *Live* to **Extract**. 
3. Switch back to your `Calgary's Population by Sector (1968-2019)` worksheet tab. Tableau will prompt you to save the local data extraction. Save the `.hyper` file in an accessible directory on your computer.
4. Navigate to the top menu bar, click **Server** → **Tableau Public** → **Save to Tableau Public...**
5. Sign in to your existing account or create a free user profile to deploy your live, interactive 50-year Calgary population trajectory online.

> 🧠 **Data Engineering Reflection:** *Tableau Public explicitly forces you to convert your connection from a "Live" data stream to a static "Extract" (.hyper file) before publishing. Why does a public cloud server prefer hosting an extract?*

## Your Finished Viz Should Look Like This:

{% include tableau-calgary.html %}


Add citations!!!




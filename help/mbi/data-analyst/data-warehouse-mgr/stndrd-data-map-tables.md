---
title: Standardize data with mapping tables
description: Learn how to work with mapping tables.
exl-id: e452ff87-f298-43d5-acc3-af58e53bd0bc
---
# Standardize Data with Mapping Tables

Picture this: you are in the `Report Builder`, building a `Revenue by State` report. You are in the zone. Everything is going swimmingly until you go to add a `billing state` grouping to your report and you see this:

![](../../assets/Messy_State_Segments.png)

## How could this happen?

Unfortunately, a lack of standardization can sometimes lead to messy data and headaches when building reports. In our example, there may not have been a dropdown menu or standardized way for our customers to input their billing state information. This lead to a variety of values - `pa`, `PA`, `penna`, `pennsylvania`, and `Pennsylvania` - all for the same state, which will certainly lead to some strange results in the `Report Builder`.

It is possible that there is a tech resource that can help you clean up the data or insert the columns you need directly into your database, but if not, we have another solution: **the mapping table**. A mapping table allows you to quickly and easily cleanse and standardize any messy data by mapping data to a single output.

>[!NOTE]
>
>You cannot create a mapping table for consolidated tables without help from our Support team. Reach out us for additional information.

## How do I create it? {#how}

**Data formatting refresher:**

* Make sure your spreadsheet has a header row.
* Avoid using commas! It will cause problems when you upload the file.
* Use the standard date format `(YYYY-MM-DD HH:MM:SS)` for dates.
* Percentages must be entered as decimals.
* Make sure any leading or trailing zeroes are properly retained.

Before you dive in, we recommend that you [export the raw table data](../../tutorials/export-raw-data.md). Looking at the raw data first means you can explore all possible combinations for the data you need to clean up, thereby ensuring that the mapping table covers everything.

To make a mapping table, you need to create a two column spreadsheet that follows the [formatting rules for file uploads](../../data-analyst/importing-data/connecting-data/using-file-uploader.md).

In the first column, enter the values stored in your database with **only one value in each row**. For example, `pa` and `PA` cannot be on the same line - each input needs to have its own row. See below for an example.

In the second column, enter what these values **should be**. Continuing with our billing state example, if we want `pa`, `PA`, `Pennsylvania`, and `pennsylvania` to simply be `PA`, we would enter `PA` in this column for each input value.

![](../../assets/Mapping_table_examples.jpg)

## What do I need to do in [!DNL MBI] to use it? {#use}

After you have finished creating the mapping table, you'll need to [upload the file](../../data-analyst/importing-data/connecting-data/using-file-uploader.md) into [!DNL MBI] and [create a joined column](../../data-analyst/data-warehouse-mgr/calc-column-types.md) that relocates the new field into the desired table. You can do this after the file is synced to your data warehouse.

In our example, we will move the column we created on the `mapping_state` table (`state_input`) to the `customer_address` table using a joined column. This will allow us to group by the clean `state_input` column in our reports instead of the `state` column.

To create the `joined` column, navigate to the table that the field will be relocated to in the Data Warehouse Manager. In our example, this would be the `customer_address` table.

1. Click **[!UICONTROL Create a Column]**.
1. Select `Joined Column` from the `Definition` dropdown.
1. Give the column a name that differentiates it from the `state` column in your database. We will go with `billing state (mapped)` so we can tell which column to use when segmenting in the report builder.
1. The path we need to connect the tables does not exist, so we need to create a new one. Click **[!UICONTROL Create new path]**  in the `Select a table and column` dropdown.

   If you are not sure what the table relationship is or how to properly define the primary and foreign keys, check out [our tutorial](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md) for some help.

   * On the `Many` side, select the table you are relocating the field to (again, for us it is `customer_address`) and the `Foreign Key` column, or `state` column, in our example.
   * On the `One` side, select the `mapping` table and the `Primary key` column. In this case, we would select the `state_input` column from the `mapping_state` table.
   * Here is a look at what our path looks like:

      ![](../../assets/State_Mapping_Path.png)

1. When finished, Click **[!UICONTROL Save]** to create the path.
1. The path may not populate immediately after saving - if this happens, click the `Path` box and select the path you just created.
1. Click **[!UICONTROL Save]** to create the column.

That is it!

## What do I do now? {#wrapup}

After an update cycle completes, you will be able to use your new joined column to properly segment your data instead of the messy column from your database. Take a look at our grouping options now - no more stress mess:

![](../../assets/Clean_State_Segments.png)

Mapping tables are handy for any time you want to clean up some potentially messy data in your data warehouse. However, mapping tables can also be used for some other cool use cases, like [replicating your Google Analytics channels in MBI](../data-warehouse-mgr/rep-google-analytics-channels.md).

### Related

* [Understanding and evaluating table relationships](../data-warehouse-mgr/table-relationships.md)
* [Creating/deleting paths for calculated columns](../data-warehouse-mgr/create-paths-calc-columns.md)

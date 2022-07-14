---
title: Standardizing data with mapping tables
zendesk_id: 360016732331
---

Picture this: you’re in the Report Builder, building a Revenue by State report. You’re in the zone. Everything is going swimmingly until you go to add a **billing state** grouping to your report and you see this:

![]({% link images/Messy_State_Segments.png %})

*How could this happen?*

Unfortunately, a lack of standardization can sometimes lead to messy data and headaches when building reports. In our example, there may not have been a dropdown menu or standardized way for our customers to input their billing state information. This lead to a variety of values - ‘pa,’ ‘PA,’ ‘penna,’ ‘pennsylvania,’ and ‘Pennsylvania’ - all for the same state, which will certainly lead to some strange results in the Report Builder.

It’s possible that there’s a tech resource that can help you clean up the data or insert the columns you need directly into your database, but if not, we have another solution: **the mapping table**. A mapping table allows you to quickly and easily cleanse and standardize any messy data by ‘mapping’ data to a single output.

{:.bs-callout-info}
You cannot create a mapping table for consolidated tables without help from our Support team. Reach out us for additional information.

## How do I create it? {#how}

**Data formatting refresher:**

* Make sure your spreadsheet has a header row.
* Avoid using commas! It’ll cause problems when you upload the file.
* Use the standard date format (YYYY-MM-DD HH:MM:SS) for dates.
* Percentages must be entered as decimals.
* Make sure any leading or trailing zeroes are properly retained.

Before you dive in, we recommend that you [export the raw table data]({% link tutorials/export-raw-data.md %}). Looking at the raw data first means you can explore all possible combinations for the data you need to clean up, thereby ensuring that the mapping table covers everything.

To make a mapping table, you’ll need to create a two column spreadsheet that follows the [formatting rules for file uploads]({{ site.baseurl}}/data-analyst/importing-data/connecting-data/using-file-uploader.html#formatting).

In the first column, enter the values stored in your database with **only one value in each row**. For example, ‘pa’ and ‘PA’ can’t be on the same line - each input needs to have its own row. See below for an example.

In the second column, enter what these values **should be**. Continuing with our billing state example, if we want ‘pa,’ ‘PA,’ ‘Pennsylvania,’ and ‘pennsylvania’ to simply be ‘PA,’ we’d enter PA in this column for each input value.

![]({% link images/Mapping_table_examples.jpg %})

## What do I need to do in Magento BI to use it? {#use}

After you’ve finished creating the mapping table, you’ll need to [upload the file]({{ site.baseurl }}/data-analyst/importing-data/connecting-data/using-file-uploader.html#uploading) into Magento BI and [create a joined column]({{ site.baseurl }}/data-analyst/data-warehouse-mgr/calc-column-types.html#joined) that relocates the new field into the desired table. You can do this after the file is synced to your data warehouse.

In our example, we’ll move the column we created on the **mapping_state** table (**state_input**) to the **customer_address** table using a joined column. This will allow us to group by the clean **state_input** column in our reports instead of the **state** column.

To create the joined column, navigate to the table that the field will be relocated to in the Data Warehouse Manager. In our example, this would be the **customer_address** table.

1. Click the **Create a Column** button.
1. Select **Joined Column** from the Definition dropdown.
1. Give the column a name that differentiates it from the state column in your database. We’ll go with **billing state (mapped)** so we can tell which column to use when segmenting in the report builder.
1. The path we need to connect the tables doesn’t exist, so we need to create a new one. Click the Create new path option in the Select a table and column dropdown.

   If you’re not sure what the table relationship is or how to properly define the primary and foreign keys, check out [our tutorial]({% link data-analyst/data-warehouse-mgr/create-paths-calc-columns.md %}) for some help.

   * On the **Many** side, select the table you’re relocating the field to (again, for us it’s **customer_address**) and the **foreign key** column, or **state** column, in our example.
   * On the **One** side, select the **mapping table** and the **primary key** column. In this case, we would select the **state_input** column from the **mapping_state** table.
   * Here's a look at what our path looks like:

      ![]({% link images/State_Mapping_Path.png %})

1. When finished, click the **Save** button to create the path.
1. The path may not populate immediately after saving - if this happens, click the **Path** box and select the path you just created.
1. Click the **Save** button to create the column.
That’s it!

## What do I do now? {#wrapup}

After an update cycle completes, you’ll be able to use your new joined column to properly segment your data instead of the messy column from your database. Take a look at our grouping options now - no more stress mess:

![]({% link images/Clean_State_Segments.png %})

Mapping tables are handy for any time you want to clean up some potentially messy data in your data warehouse. However, mapping tables can also be used for some other cool use cases, like [replicating your Google Analytics channels in Magento BI]({% link data-analyst/data-warehouse-mgr/rep-google-analytics-channels.md %}).

### Related

* [Understanding and evaluating table relationships]({% link data-analyst/data-warehouse-mgr/table-relationships.md %})
* [Creating paths for calculated columns]({% link data-analyst/data-warehouse-mgr/create-paths-calc-columns.md %})
* [Deleting calculated column paths]({% link data-analyst/data-warehouse-mgr/delete-calc-column-paths.md %})


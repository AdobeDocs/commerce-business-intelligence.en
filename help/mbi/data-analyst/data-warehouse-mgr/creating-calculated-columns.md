---
title: Create calculated columns
description: Learn how to consolidate data from different sources.
---
# Create Calculated Columns

When analyzing your data, it is beneficial to consolidate data from different sources. Want to group revenue by acquisition source, linking data from your orders table and Google Analytics? Or how about grouping revenue by customer gender, or joining a customer attribute to transaction data for segmentation?

This guide will teach you how to do just that. Before getting started, we recommend you check out the [Calculated Column Types guide](../../data-analyst/data-warehouse-mgr/calc-column-types.md). The _Calculated Column Types Guide_ outlines the types of columns you can create in the Data Warehouse Manager, along with their definitions and examples.

1. To get started, click **Manage Data** > **Data Warehouse** in the sidebar.
1. Click the table you want to create a column in. For example, if we wanted to create a **Customer Gender** column for revenue segmentation, we would select the **sales_flat_order** table.
1. The table scheme will display. Click **Create New Column**.
1. Give your column a name - for example, Customer Gender.
1. Select the definition for the column. This is where the [Calculated Column Types guide](../data-warehouse-mgr/calc-column-types.md) will come in handy!
1. For certain types of columns, a little more info is needed to properly create the column:

  * **For One to Many(joined) and Many to One (aggregate) columns**, you will need to select the tables and columns.
  * **For a Same Table calculation**, you will need to select the desired date field from the dropdown menu.
* If you are creating a One to Many (joined) or Many to One (aggregate) column, you will need to select a pathway to connect the two tables. In this step, you can either use an existing path or create a new one.

    **Remember to properly define the table as either many or one!**
  * If desired, you can apply [filters](../../data-user/reports/ess-manage-data-filters.md) to the new column.
  * When finished, click **Save**.

That is it! Your new column will appear in the current table with a Pending status. After the next update completes, your column will be available for use in metrics and reports.

## Handy reference map {#map}

If you are having a little trouble remembering what all the inputs are when creating a calculated column, try keeping this reference map handy when you are building:

![](../../assets/Calculated_Columns_Example.png)<!--{: width="805" height="643"}-->

## Related documentation

* [Calculated Column Types](../data-warehouse-mgr/calc-column-types.md)
* [Advanced Calculated Column Types](../data-warehouse-mgr/adv-calc-columns.md)
* [Building Google ECommerce dimensions with order and customer data](../data-warehouse-mgr/bldg-google-ecomm-dim.md)

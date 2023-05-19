---
title: Create calculated columns
description: Learn how to consolidate data from different sources.
exl-id: 668cbc77-6a96-4687-9f40-3635b1be5c66
---
# Create Calculated Columns

When analyzing your data, it is helpful to consolidate data from different sources. Want to group revenue by acquisition source, linking the data from your `orders` table and [!DNL Google Analytics] data? Maybe you want to group revenue by customer gender or join a customer attribute to transaction data for segmentation. This topic discusses how to do just that. 

Before getting started, Adobe recommends that you review the [Calculated Column Types Guide](../../data-analyst/data-warehouse-mgr/calc-column-types.md) for information on the types of columns that you can create in the Data Warehouse Manager, along with their definitions and examples.

1. To get started, click **[!DNL Manage Data > Data Warehouse]**.

1. Click the table in which you want to create a column. For example, if you wanted to create a `Customer Gender` column for revenue segmentation, you would select the `sales_flat_order` table.

1. The table scheme displays. Click **[!UICONTROL Create New Column]**.

1. Give your column a name. For example, `Customer Gender`.

1. Select the definition for the column. This is where the [Calculated Column Types guide](../data-warehouse-mgr/calc-column-types.md) comes in handy!

1. For certain types of columns, a little more info is needed to properly create the column:

    * For `One to Many` (joined) and `Many to One` (aggregate) columns, you need to select the tables and columns.

    * For a `Same Table calculation`, you need to select the desired date field from the dropdown.

If you are creating a `One to Many` (joined) or `Many to One` (aggregate) column, you need to select a pathway to connect the two tables. In this step, you can either use an existing path or create a one.

>[!NOTE]
>
>Remember to properly define the table as either many or one!

* If desired, you can apply [filters](../../data-user/reports/ess-manage-data-filters.md) to the new column.

* When finished, click **[!UICONTROL Save]**.

Your new column appears in the current table with a `Pending` status. After the next update completes, your column will be available for use in metrics and reports.

## Handy reference map {#map}

If you are having trouble remembering what all the inputs are when creating a calculated column, try keeping this reference map handy when you are building:

![](../../assets/Calculated_Columns_Example.png)

## Related documentation

* [Calculated Column Types](../data-warehouse-mgr/calc-column-types.md)
* [Advanced Calculated Column Types](../data-warehouse-mgr/adv-calc-columns.md)
* [Building [!DNL Google ECommerce] dimensions with order and customer data](../data-warehouse-mgr/bldg-google-ecomm-dim.md)

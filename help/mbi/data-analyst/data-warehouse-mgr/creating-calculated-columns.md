---
title: Create calculated columns
description: Learn how to consolidate data from different sources.
exl-id: 668cbc77-6a96-4687-9f40-3635b1be5c66
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/dGzhox6Xjuvc3goSxkF2W-5yBlkgKgnOJg7YcuD2Q0s
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
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

![Example calculated column configuration in Data Warehouse Manager](../../assets/Calculated_Columns_Example.png)

## Related documentation

* [Calculated Column Types](../data-warehouse-mgr/calc-column-types.md)
* [Advanced Calculated Column Types](../data-warehouse-mgr/adv-calc-columns.md)
* [Building [!DNL Google ECommerce] dimensions with order and customer data](../data-warehouse-mgr/bldg-google-ecomm-dim.md)

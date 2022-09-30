---
title: Data Warehouse Manager
description: Learn how to manage table and column sync settings, drill down into a table's schema, and create calculated columns to use in reports.
---
# Data Warehouse Manager

The Data Warehouse Manager, accessed by clicking **Manage Data > Data Warehouse** in the sidebar, is the portal to your MBI Data Warehouse. Using the Data Warehouse Manager, you can manage table and column sync settings, drill down into a table's schema, and create calculated columns to use in reports. 

>[!NOTE]
>
>You need Admin permissions to access the Data Warehouse Manager.

In this article, we will cover:

* [Learning your way around](../#learning)
* [Syncing tables and columns](../#syncing)
* [Creating calculated columns](../#calculated)
* [Dropping tables and removing columns](../#delete)
* [Syncing new tables in the background](../#syncnew)
* [So, when can I use my new columns?](../#when)

## Learning your way around {#learning}

The left side of Data Warehouse Manager page contains the tables list, allowing you to easily toggle between tables. When you select a table from the list, the table management area will populate with the table's schema where you can make changes to the selected table.

Within the table list, tables are grouped by their connection source. These sources are added under **Manage Data > Integrations** and may be either a database, an [API](https://devdocs.magento.com/mbi/docs/getting-started.html), or a third-party connector. At the top of the table list is a search box enabling you to easily find desired tables.

Underneath the search box, you will see two options: **All Tables** and **Synced Tables**. The **All Tables** option lists all the tables that you have made available to your Data Warehouse, which includes both synced and unsynced tables.

The **Synced Tables** option shows all tables that have already been added into your Data Warehouse and have data being replicated from the selected columns.

do not see the table you are looking for in the All Tables list? There are a few possible reasons for this:

* The data source has not been added yet
* The data source is a database and the MBI user you created does not have access. In this case, you or your database administrator will need to grant access.
* The data source or table was recently added and has not been synced yet

## Syncing tables and columns {#syncing}

### Syncing New Tables and Native Columns

The Data Warehouse Manager not only gives you the ability to easily view and manage your data sources, you also have the freedom to select the individual tables and columns you want to sync.

1. Click the **All Tables** option and locate the table you wish to sync.
1. Click the name of the table to preview the schema. If the table is new, all columns will display as `Unsynced`.
1. Check the columns you want to sync. Note that columns native to a table will have From Your Database in the Location column.
1. Make sure you check the **Primary Key** columns - these columns have a key symbol next to the column name. A Primary Key is required to properly sync data into the Data Warehouse.

    If you are syncing a table that comes directly from your database, it is possible that Primary Keys may not be denoted. In this case, contact your database administrator to request that a primary key or keys be added to the table.
1. When finished, click the ![button](../../assets/button.png)<!--{: width="30" height="27"}--> button.

A *Success!* message will appear and the status will change to Pending for the selected columns. After the next full update completes, the newly synced tables and columns will be available for use in reports; you can also set new [replication methods](./cfg-replication-methods.md) after the initial sync.

Here is a quick look at the whole process:

![Adding columns to your data warehouse](../../assets/DW_sync.gif)<!--{: style="max-width: 500px;"}{: data-lightbox="image-1" data-title="Adding tables and columns to your data warehouse"}-->

### Syncing New Tables in the Background {#syncnew}

When you a sync a large, new table for the first time, your data warehouse needs to retroactively capture all data points in the table before capturing new data on an ongoing basis. If your table is particularly large, you may not want to have that initial sync run in sequence with your **update cycle** — in situation, you will want the initial sync to occur in the background, in *parallel* with any currently running update.

To make sure that occurs, you should select the **Save and Sync Data Immediately** option syncing that table for the first time, as below:

![](../../assets/mceclip0.png)

### Checking for new tables and columns {#forceupdate}

Your Data Warehouse does not automatically detect new sources, tables, or columns the moment they're added. A synchronization process runs throughout the week to find new additions and make them available, but you can force a structure synchronization if you want to access newly added tables and columns before the process runs.

Below the search bar in the table list is a **Check for new tables and columns** link. Clicking this link will force-start the structure sync process; new additions are typically available after 10 minutes. Refresh the page to see the new source, table, or column.

## Creating Calculated Columns {#calculated}

Simply being able to see and manage data from all your sources makes gaining insights into your business that much easier. But within the Data Warehouse Manager, you have the ability to go a step further by creating calculated columns inside your tables. Calculated columns derive new information from your existing data.

Let us say you want to add **user's lifetime revenue** to your **users** table to find high value users. Or, if you want to segment revenue by gender, you can add **customer's gender** to your **orders** table.

To help you master creating these columns, [we created a tutorial](./creating-calculated-columns.md) to walk you through it.

## Dropping Tables and Removing Columns {#delete}

Just as you have the ability to select tables and columns to sync to your Data Warehouse, you also have the ability to drop or remove them. Note that dropping a table or removing columns will delete any dependent reports, metrics, filter sets and columns once you confirm the deletion. Be certain you want to do this - **this action cannot be undone.**

do not worry if you click Delete by accident. A dependency check runs before anything is deleted, so you will have the chance to review everything before confirming.

**To remove columns, **click the table that the column belongs to. Check the columns you want to remove and click the ![button\_1.png](../../assets/button_1.png){: width="31" height="26"} button.

**To remove a synced table**, select all columns in the table, and again click the ![button](../../assets/button_1.png)<!--{: width="31" height="26"}--> button. This will remove all native and calculated columns that use this table from your data warehouse.

### Confirming Changes

Whether you are dropping a table or removing columns, a dependency check will run before the deletion process completes. Dependencies are calculated columns, metrics, filter sets, and reports that utilize the table or column(s) being removed. Any discovered dependencies will display - at this point, you can either cancel the process or click **Confirm Changes** to drop the table/remove the column(s).

While deleted dependencies cannot be restored, the tables and columns will still be available if you need to resync any native columns in the future.

Here is a quick look at removing a column:

![Removing a column from your data warehouse](../../assets/DW_delete.gif)<!--{: style="max-width: 500px;"}{: data-lightbox="image-1" data-title="Removing a column from your data warehouse"}-->

## So, when can I use my new columns? {#when}

New synced columns and new/updated calculated columns will be ready for use after the next full update completes. If an update is not already in progress, you can force an update by clicking the **Force update** link shown at the top of the **Data Warehouse** or **Integrations** page. You can also schedule an email notification upon completion of the update by clicking **Email me when complete**.

When you are ready to use your new columns in reports, [you need to add them to metrics first](../data-warehouse-mgr/manage-data-dimensions-metrics.md). Although data will not be available until an update completes, you can still use new columns in reports. Data within the report will display when the update is finished.

## That is it - we are at the end!

We covered a lot of material in this tutorial. By now, you should have a solid understanding of what a database is, how data is organized, how tables relate to each other, and what you can do with the Data Warehouse Manager.

Excellent! Go test out your new knowledge by [creating a calculated column](../data-warehouse-mgr/creating-calculated-columns.md) or [making some interesting reports](../../tutorials/using-visual-report-builder.md).

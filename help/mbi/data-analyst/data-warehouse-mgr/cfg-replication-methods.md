---
title: Configuring replication methods
description: Learn how tables are organized, and how the table data behaves allows you to choose the best replication method for your tables.
exl-id: 83895c48-a6ec-4b01-9890-164e0b21dcbc
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Data Import/Export
---
# Configuring replication methods

`Replication` methods and [rechecks](../data-warehouse-mgr/cfg-data-rechecks.md) are used to identify new or updated data in your database tables. Setting them correctly is crucial to ensuring both data accuracy and optimized update times. This topic focuses on replication methods.

When new tables are synced in the [Data Warehouse Manager](../data-warehouse-mgr/tour-dwm.md), a replication method is automatically chosen for the table. Understanding the various replication methods, how tables are organized, and how the table data behaves allows you to choose the best replication method for your tables.

## What are the replication methods?

`Replication` methods fall into three groups - `Incremental`, `Full Table`, and `Paused`.

[**[!UICONTROL Incremental Replication]**](#incremental) means that [!DNL Commerce Intelligence] replicates only new or updated data on every replication attempt. As these methods greatly reduce latency, Adobe recommends using it where possible.

[**[!UICONTROL Full Table Replication]**](#fulltable) means that [!DNL Commerce Intelligence] replicates the entire contents of a table on every replication attempt. Because of the potentially large amount of data to be replicated, these methods can increase latency and update times. If a table contains any timestamped or datetime columns, Adobe recommends using an Incremental method instead.

**[!UICONTROL Paused]** indicates that replication for the table is stopped or paused. [!DNL Commerce Intelligence] does not check for new or updated data during an update cycle; this means that no data is replicated from a table that has this as its Replication Method.

## Incremental replication methods {#incremental}

### Modified At (most ideal)

The `Modified At` replication method uses a datetime column - which is populated when a row is created and then updated when data changes - to find data to replicate. This method is designed to work with tables that meet the following criteria:

* contains a `datetime` column that is initially populated when a row is created and is updated whenever the row is modified;
* the `datetime` column is never null;
* rows are not deleted from the table

In addition to those criteria, Adobe recommends **indexing** the `datetime` column used for `Modified At` replication, as this helps optimize replication speed.

When the update runs, new or changed data is identified by searching for rows that have a value in the `datetime` column that occurred after the most recent update. When new rows are discovered, they are replicated to your Data Warehouse. If any rows exist in the [Data Warehouse Manager](../data-warehouse-mgr/tour-dwm.md), they are overwritten with the current database values.

For example, a table may have a column called `modified\_at` that indicates the last time data was changed. If the most recent update ran Tuesday at noon, the update searches for all rows having a `modified\_at` value greater than Tuesday at noon. Any discovered rows that were either created or modified since noon on Tuesday are replicated to the Data Warehouse.

**Did you know?**
Even if your database cannot currently support an `Incremental` Replication method, you may be able to [make changes to your database](../../best-practices/mod-db-inc-replication.md) that would enable use of `Modified At` or `Single Auto Incrementing PK`.

`Modified At` is not only the most ideal replication method, it is also the fastest. This method not only produces noticeable speed increases with large data sets, it also does not require configuring a recheck option. Other methods need to iterate through an entire table to identify changes, even if a small subset of data has changed. `Modified At` iterates through only that small subset.

### Single Auto Incrementing Primary Key

`Auto Incrementing` is a behavior that sequentially assigns primary keys to rows. If a table is `Auto Incrementing` and the highest primary key in the table is 1,000, then the next primary value is 1,001 or higher. A table that does not use `Auto Incrementing` behavior may assign a primary key value that is less than 1,000 or jump to a much bigger number, but this is not commonly used.

This method is designed to replicate new data from tables that meet the following criteria:

* `single-column primary key`; and
* `primary key` datatype is `integer`; and
* `auto incrementing` primary key values.

When a table is using `Single Auto Incrementing Primary Key` replication, new data is discovered by searching for primary key values that are higher than the current highest value in your Data Warehouse. For example, if the highest primary key value in your Data Warehouse is 500, when the next update runs it will search for rows with primary key values of 501 or higher.

### Add Date

The `Add Date` method functions similarly to the `Single Auto Incrementing Primary Key` method. Instead of using an integer for the table's primary key, this method uses a `timestamped` column to check for new rows.

When a table uses `Add Date` replication, new data is discovered by searching for timestamped values that are greater than the latest date synced to your Data Warehouse. For example, if an update last ran on 20/12/2015 09:00:00, any rows with a timestamp greater than this will be marked as new data and replicated.

>[!NOTE]
>
>Unlike the `Modified At` method, `Add Date` does not check existing rows for updated information - it only looks forward to new rows.

## Full table replication methods {#fulltable}

### Full Table

`Full table` replication refreshes the entire table any time new rows are detected. This is by far the least efficient replication method, because all data must be reprocessed during every update, assuming there are new rows.

New rows are detected by querying your database at the start of the synchronization process and counting the number of rows. If your local database contains more rows than [!DNL Commerce Intelligence], then the table is refreshed. If the row counts are identical, or if [!DNL Commerce Intelligence] contains *more* rows than your local database, then the table is skipped.

This raises the important point that **`Full Table` replication is incompatible when:**

* more rows are deleted than created in your local database table between subsequent update cycles, or
* column values are changed, but no additional rows are created

In either of the above scenarios, `Full Table` replication does not detect any changes and your data becomes stale. Due to the inefficiency of this replication method, and the requirements mentioned above, `Full Table` replication is only recommended as a last resort.

### Primary Key Batch

When a table uses `Primary Key Batch` (PK Batch), new data is discovered by counting rows inside ranges, or batches, of primary key values. While you typically think of this being used with integers, even text values can be ordered in a way that allows the system to define constant ranges.

For example, say that an update runs and performs a row count for the range of keys from 1 to 100. In this update, the system finds and logs 37 rows. In the next update, a row count is performed again on the 1-100 range and finds 41 rows. Because there is a difference in the number of rows compared to the last update, the system inspects that range (or batch) in more detail.

This method is intended to replicate data from tables that meet the following criteria:

* single-column non-integer; or
* composite keys (multiple columns comprising the primary key) - note that columns used in a composite primary key can never have null values; or
* single-column, integer, non-auto-incrementing primary key values.

This method is not ideal, as it is incredibly slow due to the amount of processing that must occur to examine batches and find changes. Adobe recommends not using this method unless it is impossible to make necessary modifications to support the other replication methods. Expect update times to increase if this method must be used.

## Setting replication methods

Replication methods are set on a table-by-table basis. To set a replication method for a table, you need [`Admin`](../../administrator/user-management/user-management.md) permissions so you can access the Data Warehouse Manager.

1. Once in the Data Warehouse Manager, select the table from the `Synced Tables` list to display the table's schema.
1. The current replication method is listed below the table name. To change it, click the link.
1. In the pop-up that displays, click the radio button next to either `Incremental` or `Full Table` replication to select a replication type.
1. Next, click the **[!UICONTROL Replication Method]** dropdown to select a method. For example, `Paused` or `Modified At`.

   >[!NOTE]
   >
   >**Some Incremental methods require you to set a `Replication Key`**. [!DNL Commerce Intelligence] will use this key to determine where the next update cycle should begin.
   >
   >For example, if you want to use the `modified at` method for your `orders` table, you need to set a `date column` as the replication key. Several options for replication keys may exist, but you select `created at`, or the time the order was created. If the last update cycle stopped at 12/1/2015 00:10:00, the next cycle would begin replicating data with a `created at` date greater than this.

1. When finished, click **[!UICONTROL Save]**.

Look at the whole process:

![](../../assets/replication_method.gif)<!--{: width="801" height="341"}-->

## Wrapping up

To finish up, you have put together this table that compares the various replication methods. It is incredibly handy when selecting a method for the tables in your Data Warehouse.

| **`Method`** | **`Syncing New Data`** | **`Processing Rechecks on Large Data Sets`** | **`Handle Composite Keys?`** | **`Handle Non-Integer PKs?`** | **`Handle Non-Sequential PK Population?`** | **`Handle Row Deletion?`** |
|-----|-----|-----|-----|-----|-----|-----|
| `Auto-Incrementing Primary Key` | Faster | Slow | No | No | No | Yes |
| `Primary Key Batch Monitoring` | Slow | Slow | Yes | Yes | Yes | Yes |
| `Modified At` | Faster | Faster | Yes | Yes | Yes | No |

{style="table-layout:auto"}

## Related documentation

* [Understanding data rechecks](../data-warehouse-mgr/cfg-data-rechecks.md)
* [Modifying your database to support `Incremental` Replication](../../best-practices/mod-db-inc-replication.md)
* [Optimizing your database for analysis](../../best-practices/opt-db-analysis.md)
* [Reducing Update Times](../../best-practices/reduce-update-cycle-time.md)

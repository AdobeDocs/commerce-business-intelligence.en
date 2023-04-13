---
title: Modifying Your Database to Support for Incremental Replication
description: Learn how to modify your database to support incremental replication.
exl-id: c9a38892-6096-4eb5-8a53-35b8b7b083dc
---
# Support for Incremental Replication

If your tables currently do not allow for incremental replication, refer to the following recommendations for possible solutions.

## Modifications for Modified At

The `Modified At` method, which is the most ideal replication method, uses a `datetime` column to detect new and/or updated data. Remember that the `datetime` column in tables using this method must be indexed and cannot contain null values at any time.

If your table does not have a `datetime` column, you can add an index `modified at` column. Null values are not allowed in a `modified at` column. Check that the column is populated for every row.

To ensure the `Modified At` method works as intended, you cannot delete rows from the table. Rather, you should mark the row as invalid by adding a `deleted` column to the table. This column returns a `1` if the row is invalid and `0` otherwise. You can then use this column to filter out invalid rows when you are building metrics and reports.

## Modifications for Single Auto Incrementing Primary Key

If the `Modified At` method cannot be enabled, then the Single Auto Incrementing Primary Key is the next best option. New data is discovered in tables using this method by searching for primary key values that are higher than the current highest value in the Data Warehouse.

Remember, tables using this method are single column with integer auto incrementing primary keys. To use this method in your database, make the following modifications:

* If the primary key is either a composite key or a non-integer, change the primary key to an auto incrementing integer
* If the primary key is a single integer column but keys can be assigned non-sequentially, change the primary key to auto increment

## Wrapping Up

By making minor modifications to your tables, you can take advantage of the faster, more efficient Incremental Replication Methods. However, if this is not possible, you can still take other steps to [reduce your update time](../best-practices/reduce-update-cycle-time.md) and [optimize your database](../best-practices/opt-db-analysis.md).

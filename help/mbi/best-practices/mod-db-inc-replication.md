---
title: Modifying Your Database to Support for Incremental Replication
description: Learn how to modify your database to support incremental replication.
exl-id: c9a38892-6096-4eb5-8a53-35b8b7b083dc
role: Admin, Developer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
TQID: https://experienceleague.adobe.com/VH5mhfRJteAxiQAmh14TzhnAqym65X6SFRMGuSuEvwM
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
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

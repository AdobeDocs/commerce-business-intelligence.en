---
title: Event Number Calculated Column
description: Learn the purpose and uses of the Event Number calculated column.
exl-id: c234621e-2e68-4e63-8b0d-7034d1b5fe1f
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/vLN8AubwPn0Cq0CmmVq4nHbWNjWrCZNBvfhSDsE6lBw
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
# Event Number Calculated Column

This topic outlines the purpose and uses of the `Event Number` calculated column available in the **[!DNL Manage Data > Data Warehouse]** page. Below is an explanation of what it does, followed by an example, and the mechanics of creating it.

**Explanation**

The `Event Number` column type identifies the sequence in which events occurred for a particular **event owner**, like a `customer` or `user`. If you are familiar with SQL, this column type is identical to the `RANK` function. It could be used to observe differences in behavior between first-time events, repeat events, or nth events in your data.

In cases of a tie, this column contains the same **rank** for the tied events, and skips the subsequent numbers. For example, if it were ranking the numbers 5,8,10,10,12, the ranks would be 1,2,3,3,5.

The most common use case of this column is to analyze first time buyers and repeat buyers. First time buyers are identified by adding a filter (to a metric or report) on `Customer's order number` = 1. `Customer's order number` is a column of the type `Event Number`.

**Example**

|**`event_id`**|**`owner_id`**|**`timestamp`**|**`Owner's event number`**|
|--- |--- |--- |--- |
|**1|A|2015-01-01 00:00:00|1|
|**2|B|2015-01-01 00:30:00|1|
|**3|A|2015-01-01 02:00:00|2|
|**4|A|2015-01-02 13:00:00|3|
|**5|B|2015-01-03 13:00:00|2|

In the above example, the column `Owner's event number` is an `Event Number` column. It ranks the owner's events in the order in which they occurred (based on the `timestamp` column).

For instance, consider all rows where `owner_id = A`. The first row in the table is the earliest timestamp for this owner, followed by the third row in the table, followed by the fourth row in the table.

**Mechanics**

Here are some instructions on creating an `Event Number` column:

1. Navigate to the **[!UICONTROL Manage Data > Data Warehouse]** page.

1. Navigate to the table on which you want to create this column.

1. Click **[!UICONTROL Create a Column]** and choose the `EVENT_NUMBER (…)` column type: under the `Same Table` section.

1. The first dropdown `Event Owner` specifies the entity for which the rank is to be determined. In the case where a `Customer's order number`, a customer identifier such as `customer_id` or `customer_email` would be the `Event Owner`.

1. The second dropdown `Event Rank` specifies the column that enforces the sequence that determines the rank of the row. In the case where a `Customer's order number`, the `created_at` timestamp would be the `Event Rank`.

1. Under the `Options` dropdown, you can add filters to exclude rows from being considered. The excluded rows have a `NULL` value for this column.

1. Provide a name to the column and Click **[!UICONTROL Save]**.

1. The column is available to use _immediately._

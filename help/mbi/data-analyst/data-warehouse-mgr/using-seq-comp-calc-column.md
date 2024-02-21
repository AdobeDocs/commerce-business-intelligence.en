---
title: Sequential Comparison Calculated Column
description: Learn the purpose and uses of the Sequential Comparison calculated column.
exl-id: 625062b4-f05d-42aa-94c3-729b39c7d728
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
---
# Sequential Comparison Calculated Column

This topic outlines the purpose and uses of the `Sequential Comparison` calculated column available in the **[!DNL Manage Data > Data Warehouse]** page. Below is an explanation of what it does, followed by an example and the mechanics of creating it.

**Explanation**

The `Sequential Comparison` column type: finds the difference between consecutive events. The most common type of `Sequential Comparison` column is the `Seconds since previous order` column. There are three inputs needed for this column:

1. `Event Owner`: This input determines the entity for which rows are grouped. For example, in the `Seconds since previous order` column, the event owner is the customer, because you want to find the number of seconds since the previous order of the same customer.
1. `Event Date`: This input enforces the sequence of events. In the cases of `Seconds since previous order`, the column containing the timestamp of the order should be the `Event Date`. This input is always a timestamp.
1. `Value to Compare`: This input is the actual value to be compared. It subtracts the previous row's value from the current row's value. Hence, a column finding the time difference between successive orders of a customer is called `Seconds since previous order`. This input does not have to be a timestamp. A non-timestamp example is to find the difference in order value between successive orders of a customer.

**Example**

|**`event_id`**|**`owner_id`**|**`timestamp`**|**`Seconds since owner's previous event`**|
|--- |--- |--- |--- |
|**`1`**|A|2015-01-01 00:00:00|NULL|
|**`2`**|B|2015-01-01 00:30:00|NULL|
|**`3`**|A|2015-01-01 02:00:00|7200|
|**`4`**|A|2015-01-02 13:00:00|126000|
|**`5`**|B|2015-01-03 13:00:00|217800|

 In the above example, `Seconds since owner's previous event` is the `Sequential Comparison` calculated column. For the `owner_id = A`, it first identifies a sequence based on the `timestamp` column, and then subtracts the previous event's `timestamp` from the current event's timestamp. In the third row in the table – the second row for `owner_id A` – the value of `Seconds since owner's previous event` is the number of seconds between '2015-01-01 02:00' and '2015-01-01 00:00:00'. This difference equals two hours = 7200 seconds.

For this calculated column type, the row corresponding to the owner's first event has a `NULL` value.

**Mechanics**

To create an **Event Number** column:

1. Navigate to the **[!DNL Manage Data > Data Warehouse]** page.

1. Navigate to the table on which you want to create this column.

1. Click **[!UICONTROL Create New Column]** in the upper-right corner.

1. Select `Same Table` as the `Definition Type` (if the columns that you want to compare are not on the same table you may need to relocate them).

1. Select `SEQUENTIAL_COMPARISON` as the `Column Definition Equation`.

1. Choose the inputs, as explained above:
   - `Event Owner`
   - `Event Date`
   - `Value to Compare`

1. Filters can also be added to exclude rows from being considered. The excluded rows have a `NULL` value for this column.

1. Provide a name for the column at the top of the page and click **[!UICONTROL Save]**.

1. The column is available to use *immediately*.

![SEC](../../assets/SEC_new.png)

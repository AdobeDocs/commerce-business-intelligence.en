---
title: Using the Date Difference Calculated Column
description: Learn the purpose and uses of the Date Difference calculated column.
exl-id: 6ecab794-3466-4b3a-a929-3e56287522aa
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/5SElfBoU6vqCNthFdj96eCNH26dC54ucjqknnhQXQy8
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
# Date Difference Calculated Column

 This topic outlines the purpose and uses of the `Date Difference` calculated column available in the **[!DNL Manage Data > Data Warehouse]** page. Below is an explanation of what it does, followed by an example, and the mechanics of creating it.

**Explanation**

The `Date Difference` column type calculates the time between two events belonging to a single record, based on the event timestamps. The raw value calculated in this column is in seconds, but it auto-converts to minutes, hours, days, and so on, for display on reports. When used as a filter/group by, however, you want to use the value in seconds.

A `date difference` calculated column can be used to create a metric which calculates the average or median time between two events, such as average time between customer registration and their first orders.

**Example**

|**`id`**|**`timestamp_1`**|**`timestamp_2`**|**`Seconds between timestamp_2 and timestamp_1`**|
|--- |--- |--- |--- |
|`A`|2015-01-01 00:00:00|2015-01-01 12:30:00|45000|
|`B`|2015-01-01 08:00:00|2015-01-01 10:00:00|7200|

{style="table-layout:auto"}


In the above example, the `Date Difference` column is the `Seconds between timestamp_2 and timestamp_1` column. It performs the calculation `timestamp_2 minus timestamp_1`.

**Mechanics**

The following steps describe how to create a `Date Difference` column.

1. Navigate to the **[!DNL Manage Data > Data Warehouse]** page.
1. Navigate to the table on which you want to create this column.
1. Click **[!UICONTROL Create a Column]** and configure your column as follows:
    * Select `Column Definition Type` > `Same Table`
    * Select `Column Definition Equation` > `DATE_DIFF = (Ending DATETIME - Starting DATETIME)`
    * Select `Ending DATETIME` column > Choose the ending datetime field, which is typically the event that occurs later
    * Select `Starting DATETIME` column** > Choose the starting datetime field, which is typically the event that occurs earlier

1. Provide a name to the column and click **[!UICONTROL Save]**.
1. The column is available to use *immediately*.

As an example, the following example is configured to calculate the `Seconds between order date and customer's creation date`:

![Date difference calculation configuration showing datetime column selections](../../assets/date_diff.png)

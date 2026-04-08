---
title: Configuring Data Checks
description: Learn how to configure data columns with changeable values.
exl-id: c31ef32e-ba5a-4902-b632-fbab551cc632
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager
TQID: https://experienceleague.adobe.com/aw43nDwCdBOJ-9D2BKJGV7PV-7c3jGXxhUEgE2utY5A
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
# Configuring Data Checks

In a database table, there can be data columns with changeable values. For example, in an `orders` table there might be a column called `status`. When an order is initially written to the database, the status column might contain the value _pending_. The order is replicated in your [Data Warehouse](../data-warehouse-mgr/tour-dwm.md) with this `pending` value.

Order statuses can change, though they are not always in a `pending` status. Eventually it could become `complete` or `cancelled`. To ensure that your Data Warehouse syncs this change, the column must be rechecked for new values.

How does this fit in with the [replication methods](../data-warehouse-mgr/cfg-replication-methods.md) that was discussed? The processing of rechecks varies based on the chosen replication method. The `Modified\_At` replication method is the best choice for processing changing values, as rechecks do not have to be configured. The `Auto-Incrementing Primary Key` and `Primary Key Batch Monitoring` methods require recheck configuration.

When using either of these methods, changeable columns must be flagged for rechecking. There are three ways to do this:

1. An auditing process that runs as part of the update flags columns to be rechecked. 

   >[!NOTE]
   >
   >The auditor relies on a sampling process and the changing columns may not be caught immediately.

1. You can set them yourself by selecting the checkbox next to the column in the Data Warehouse manager, clicking **[!UICONTROL Set Recheck Frequency]**, and choosing an appropriate time interval for when you should check for changes.

1. A member of the [!DNL Adobe Commerce Intelligence] Data Warehouse team can manually mark the columns for rechecking in your Data Warehouse. If you are aware of changeable columns, contact the team to request that rechecks are set. Include a list of columns, along with frequency, with your request.

## Recheck frequencies {#frequency}

**Did you know?**
Setting a recheck on a `primary key` column does not check the column for changed values. The table is checked for deleted rows and any deletions are purged from the Data Warehouse.

When a column is flagged for rechecking, you can also set how often a recheck occurs. If a particular column does not change often, choosing a less frequent recheck can [optimize your update cycle](../../best-practices/reduce-update-cycle-time.md).

Frequency options are:

* `always` - recheck occurs during every update
* `daily` - recheck occurs first post-midnight update for your declared timezone
* `weekly` - recheck occurs post-9pm Friday update every week for your declared timezone
* `monthly` - recheck occurs post-9pm Friday update every four weeks for your declared timezone
* `once` - occurs only in the next update (a one-off refresh)

As update times are correlated to how much data needs to be synced, Adobe recommends choosing a `daily`, `weekly`, or `monthly` recheck instead of every update.

## Managing recheck frequencies {#manage}

Recheck frequencies can be managed in the Data Warehouse by clicking a table name and then checking individual columns. The syncing status and recheck frequency (the **Changes?** column) displays for each column in the table.

To change the recheck frequency, click the checkbox next to the columns you want to change. Then click the **[!UICONTROL Set Recheck Frequency]** dropdown and set the desired frequency.

![Data Warehouse Manager showing recheck configuration options](../../assets/dwm-recheck.png)

You might sometimes see `Paused` in the `Changes?` column. This value displays when the table's [replication method](../../data-analyst/data-warehouse-mgr/cfg-data-rechecks.md) is set to `Paused`.

[!DNL Adobe] recommends reviewing these columns to both optimize your updates and ensure that changeable columns are being rechecked. If the recheck frequency for a column is high given how often the data changes, Adobe recommends decreasing it to optimize your updates.

Contact us with questions or to inquire about current replication methods or rechecks.

**Related:**

* [Reducing Update Times](../../best-practices/reduce-update-cycle-time.md)
* [Optimizing your Database for Analysis](../../best-practices/opt-db-analysis.md)

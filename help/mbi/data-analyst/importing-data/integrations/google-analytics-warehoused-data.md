---
title: Expected Google Analytics Warehoused Data
description: Learn to interact with your Google Analytics warehoused data.
exl-id: 2b1305cd-5f34-43d9-b77f-a4f5b1d82c66
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
---
# Expected [!DNL Google Analytics Warehoused] Data

>[!NOTE]
>
>Requires [Admin permissions](../../../administrator/user-management/user-management.md).

>[!NOTE]
>
>Some information was used with permission from your friends at [[!DNL Stitch]](https://www.stitchdata.com/docs/integrations/saas/google-analytics).

[!DNL Google Analytics Warehoused] integration in [!DNL Commerce Intelligence] uses the [!DNL Google Analytics] [Core Reporting API](https://developers.google.com/analytics/devguides/reporting/core/v3/).

>[!NOTE]
>
>To avoid unexpected or nonsensical results, confirm that any dimensions you use are [compatible with one or more metrics](https://ga-dev-tools.google/dimensions-metrics-explorer/) you use in the `Report Builder`. 

A single table - called `report` - is created in your Data Warehouse.

The schema of this table is composed of the Metrics and Dimensions that you selected during the setup process and two other columns: `start-date` and `end-date`.

If for example, you selected the following Metrics and Dimensions during setup:

* `Metrics`: `ga:users`
* `Dimensions`: `ga:month`

The table would look like the example below.

| **Column Name** | **Description** |
|-----|-----|
| `\_id` | This column is the `primary key`. |
| `\_rjm\_record\_hash` | [!DNL Commerce Intelligence] unique identifier. This column is created by [!DNL Commerce Intelligence]. |
| `\_updated\_at` | This column contains the last time that the data row was updated. This column is created by [!DNL Commerce Intelligence]. |
| `start-date` | Identification of what day the row is for. |
| `end-date` | Identification of what day the row is for. |
| `month` | Selected dimension: Month of the session, a two-digit integer from 01 to 12. |
| `users` | Selected metric: The total number of users for the requested time period. |

{style="table-layout:auto"}

## What's the difference between [!DNL Google Analytics Warehoused] and [!DNL Live Integration]

The main differentiator is that one integration is stored ([!DNL Google Analytics Warehoused]), and the other is not ([!DNL Google Analytics Live]). In cases of [!DNL Google Analytics Warehoused], this allows for manipulation of your [!DNL Google Analytics] data and gives you the ability to combine [!DNL Google Analytics] and other data sources to create insightful reporting.

Look at [!DNL Google Analytics] ad campaigns for an example of what can be done from a manipulation standpoint. Suppose you had multiple ad campaigns for Q4 with different names. The campaigns were a result of a specific marketing initiative. With warehoused data, you can create a column that finds the campaign names in question and returns the Q4 initiative name of `Operation Dumbo`.

The combination aspect allows [!DNL Google Analytics] data to be joined to other data in order to conduct analyses. For example, take `Total Time On Site By Ad Campaign` data from [!DNL Google Analytics] and join it up against `Total Spent Per Campaign` data from [!DNL Facebook Ads] to get a complete picture of how much engagement is costing you.

With the [!DNL Google Analytics Live] integration on the other hand, every [!DNL Google Analytics] chart is like a little silo that is not stored in your [!DNL Commerce Intelligence] Data Warehouse.

## Related:

* [Connecting [!DNL Google Analytics Warehoused]](../integrations/google-analytics-warehoused.md)

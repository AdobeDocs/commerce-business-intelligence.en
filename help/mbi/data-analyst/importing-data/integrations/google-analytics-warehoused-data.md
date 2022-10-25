---
title: Expected Google Analytics Warehoused Data
description: Learn to interact with your Google Analytics warehoused data.
---
# Expected Google Analytics Warehoused Data

>[!NOTE]
>
>[Requires Admin permissions.](../../../administrator/user-management/user-management.md)

**Some information was used with permission from our friends at [Stitch](https://www.stitchdata.com/docs/integrations/saas/google-analytics).**

Google Analytics Warehoused integration in [!DNL MBI] utilizes the Google Analytics [Core Reporting API](https://developers.google.com/analytics/devguides/reporting/core/v3/).

>[!NOTE]
>
>To avoid unexpected or nonsensical results, confirm that any dimensions you use are compatible with the metric(s) you use in the Report Builder. You can check [here](https://developers.google.com/analytics/devguides/reporting/core/dimsmets).

A single table - called `report` - will be created in your Data Warehouse.

The schema of this table will be composed of the Metrics and Dimensions you selected during the setup process and two other columns:` start-date` and `end-date`.

If, for example, you selected the following Metrics and Dimensions during setup:

* **Metrics**\: `ga:users`
* **Dimensions**\: `ga:month`

The table would look like the example below.

| **Column Name** | **Description** |
|-----|-----|
| \_id | This column is the primary key. |
| \_rjm\_record\_hash | [!DNL MBI] unique identifier. This column is created by [!DNL MBI]. |
| \_updated\_at | This column contains the last time that the data row was updated. This column is created by [!DNL MBI]. |
| start-date | Identification of what day the row is for. |
| end-date | Identification of what day the row is for. |
| month | Selected dimension: Month of the session, a two digit integer from 01 to 12. |
| users | Selected metric: The total number of users for the requested time period. |

{style="table-layout:auto"}

## Reminder: Difference between Google Analytics Warehoused and Live Integration

The main differentiator is that one integration is stored (Google Analytics Warehoused), and the other is not (Google Analytics Live). In the case of Google Analytics Warehoused, this allows for manipulation of your Google Analytics data and gives you the ability to combine Google Analytics and other data sources to create insightful reporting.

Let us look at Google Analytics ad campaigns for an example of what can be done from a manipulation standpoint. Suppose you had multiple ad campaigns for Q4 with different names. The campaigns were a result of a specific marketing initiative. With warehoused data, we can create a new column that finds the campaign names in question and returns the Q4 initiative name of "Operation Dumbo".

The combination aspect allows Google Analytics data to be joined to other data in order to conduct analyses. For example, take "Total Time On Site By Ad Campaign" data from Google Analytics and join it up against "Total Spent Per Campaign" data from Facebook Ads to get a complete picture of how much engagement is costing you.

With the Google Analytics Live integration on the other hand, every Google Analytics chart is like a little silo that is not stored in your [!DNL MBI] data warehouse.

## Related:

* [Connecting Google Analytics Warehoused](../integrations/google-analytics-warehoused.md)

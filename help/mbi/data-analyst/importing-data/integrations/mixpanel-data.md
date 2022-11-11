---
title: Expected Mixpanel data
description: Explore the main data tables that you can import from Mixpanel into your [!DNL MBI] account.
exl-id: 87bd337a-63fa-44cf-b1fe-c2f34ca86029
---
# Expected [!DNL Mixpanel] data

After [you have connected your [!DNL Mixpanel] account](../integrations/mixpanel.md), you can use the [Data Warehouse Manager](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) to easily track relevant data fields for analysis.

In this article, we explore the main data tables that you can import from [!DNL Mixpanel] into your [!DNL MBI] account. The following tables will be created in your data warehouse after connecting Mixpanel. To view all the fields available for tracking, click the links in the table name column.

>[!NOTE]
>
>Due to the limitations of the [!DNL Mixpanel] API, historical data - data older than seven (7) days from the date of connection to [!DNL MBI] - will not be replicated.

| **Table Name** | **Description** |
|-----|-----|
| [`mixpanel\_export`](https://mixpanel.com/docs/api-documentation/exporting-raw-data-you-inserted-into-mixpanel#datafeed) | This table contains raw event data, including the event, event dates, and platform bucket. |
| [`mixpanel\_funnels`](https://mixpanel.com/docs/api-documentation/data-export-api#funnels-default) | This table contains data about your funnels, including the funnel ID, the funnel length (# of days the user has to complete the funnel), and the starting and ending dates of the funnel. |
| [`mixpanel\_engage`](https://mixpanel.com/docs/api-documentation/data-export-api#engage-default) | This contains data from People Analytics, including session IDs, page and user information, and the date/time the user was last seen.  |

{style="table-layout:auto"}

## Related documentation

* [Connecting [!DNL Mixpanel]](../integrations/mixpanel.md)
* [Reauthenticating integrations](https://support.magento.com/hc/en-us/articles/360016733151-Reauthenticating-integrations)

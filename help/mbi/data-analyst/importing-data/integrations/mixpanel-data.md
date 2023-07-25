---
title: Expected Mixpanel data
description: Explore the main data tables that you can import from Mixpanel into your [!DNL Commerce Intelligence] account.
exl-id: 87bd337a-63fa-44cf-b1fe-c2f34ca86029
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
---
# Expected [!DNL Mixpanel] data

After [you have connected your [!DNL Mixpanel] account](../integrations/mixpanel.md), you can use the [Data Warehouse Manager](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) to easily track relevant data fields for analysis.

This topic explores the main data tables that you can import from [!DNL Mixpanel] into your [!DNL Commerce Intelligence] account. The following tables will be created in your Data Warehouse after connecting [!DNL Mixpanel]. To view all the fields available for tracking, click the links in the table name column.

>[!NOTE]
>
>Due to the limitations of the [!DNL Mixpanel] API, historical data - data older than seven (7) days from the date of connection to [!DNL Commerce Intelligence] - is not replicated.

| **Table Name** | **Description** |
|-----|-----|
| [`mixpanel\_export`](https://developer.mixpanel.com/reference/raw-data-export-api#datafeed) | This table contains raw event data, including the event, event dates, and platform bucket. |
| [`mixpanel\_funnels`](https://developer.mixpanel.com/reference/raw-data-export-api#funnels-default) | This table contains data about your funnels, including the funnel ID, the funnel length (# of days the user has to complete the funnel), and the starting and ending dates of the funnel. |
| [`mixpanel\_engage`](https://developer.mixpanel.com/reference/raw-data-export-api#engage-default) | This contains data from People Analytics, including session IDs, page and user information, and the date/time the user was last seen.  |

{style="table-layout:auto"}

## Related documentation

* [Connecting [!DNL Mixpanel]](../integrations/mixpanel.md)
* [Reauthenticating integrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)

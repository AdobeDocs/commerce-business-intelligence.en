---
title: Expected Mixpanel data
description: Explore the main data tables that you can import from Mixpanel into your [!DNL Commerce Intelligence] account.
exl-id: 87bd337a-63fa-44cf-b1fe-c2f34ca86029
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/iM6GzisImrjed7uCZf6lf6HIze9MwWdhq2gEP-IrIXA
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

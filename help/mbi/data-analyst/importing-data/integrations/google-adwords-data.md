---
title: Expected Google Adwords data
description: Learn how you can use the Data Warehouse Manager to easily track relevant data fields for analysis.
exl-id: b0085683-7bb1-4da2-b343-4309e4796f0c
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/iCKOCRAELybmKfHS8F7XaKpEx9blpkRK0i0e-eEYJgU
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
  - id: f42e0a1a-0d79-488d-a83f-f2c30672b137
    internal-label: Reporting
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
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
    internal-label: Reporting
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
---
# Expected [!DNL Google Adwords] data

After [you have connected your [!DNL Google Adwords] account](../integrations/google-adwords.md), you can use the [Data Warehouse Manager](../../data-warehouse-mgr/tour-dwm.md) to easily track relevant data fields for analysis.

There, you notice two tables available for replication into your Data Warehouse:

* `campaigns[account-id]` 
* `adwords[account-id]`

The `campaigns` table *should be used by default*, so you can begin by syncing all relevant fields from that table.

The `adwords` table contains four columns that are not in the `campaigns` table:

1. `keyword`
1. `adContent`
1. `adDestinationUrl`
1. `adGroup`

Whenever you are interested in performing an analysis that considers these attributes, you must use the `adwords` table. 

>[!IMPORTANT]
>
>This table excludes rows where all four of these columns are `null`.

Below is a look at the expected schema for both tables.

## [!DNL Campaigns] table

The `campaigns` table contains the following columns:

| **Column** | **Description** |
|-----|-----|
| `\_id` | The primary key for the table  |
| `accountId` | The account ID |
| [`adClicks`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adclicks) | Total number of clicks for the day |
| [`adCost`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adcost) | Total cost for the campaign for the day |
| [`adwordsCampaignID`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adwordscampaignid) | [!DNL Adwords] Campaign ID |
| [`campaign`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=traffic_sources&jump=ga_campaign) | Campaign name (for example, [utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)) |
| [`date`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=time&jump=ga_date) | The date the campaign ran |
| [`impressions`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_impressions) | Number of impressions for the day |
| `profileId` | The profile ID |
| `profileName` | The profile name |
| `\_updated\_at` | The date and time of the last update for this row |

{style="table-layout:auto"}

## [!DNL AdWords] table

The `adwords` table contains the following columns:

| **Column** | **Description** |
|-----|-----|
| `\_id` | The primary key for the table  |
| `accountId` | The account ID |
| [`adClicks`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adclicks) | Total number of clicks for the day |
| [`adCost`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adcost) | Total cost for the campaign for the day |
| [`adwordsCampaignID`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adwordscampaignid) | [!DNL Adwords] Campaign ID |
| [`campaign`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=traffic_sources&jump=ga_campaign) | Campaign name (for example, [utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)) |
| [`date`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=time&jump=ga_date) | The date the campaign ran |
| [`impressions`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_impressions) | Number of impressions for the day |
| `profileId` | The profile ID |
| `profileName` | The profile name |
| `\_updated\_at` | The date and time of the last update for this row |
| `keyword` | The keyword of the campaign |
| `adContent` | The first line of the text for the online campaign |
| `adDestinationUrl` | The URL to which the [!DNL Adwords] ads referred traffic |
| `adGroup` | The name of the [!DNL Adwords] ad group |

{style="table-layout:auto"}

Using this data, you can start creating [metrics](../../../data-user/reports/ess-manage-data-metrics.md) and [reports](../../../tutorials/using-visual-report-builder.md) based on spending data and [marry it to your lifetime revenue to calculate ROI](../../analysis/roi-ad-camp.md).

## Consolidated tables

[!DNL Adobe] recommends creating a `consolidated ad spend` table to combine the data from all of your multiple advertising sources into a single table. This enables you to use a single set of metrics for advertising analysis.

If you do not have a consolidated table and you build a beautiful dashboard on the `adwords` table, you need to replicate the reporting or create duplicate metrics to compare that data to your [!DNL Facebook Ads] data. Using a consolidated table allows you to seamlessly incorporate [!DNL Facebook Ads] data with your existing [!DNL Adwords] reports. You can segment by ad platform as well.

If you have already synced the fields above, [contact us](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) to consolidate your ad spend.

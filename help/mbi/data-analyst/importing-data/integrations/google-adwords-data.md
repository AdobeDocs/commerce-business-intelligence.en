---
title: Expected Google Adwords data
description: Learn how you can use the Data Warehouse Manager to easily track relevant data fields for analysis.
---
# Expected Google Adwords data

After [you have connected your [!DNL Google Adwords] account](../integrations/google-adwords.md), you can use the [Data Warehouse Manager](../../data-warehouse-mgr/tour-dwm.md) to easily track relevant data fields for analysis.

There, you notice two tables available for replication into your data warehouse: `campaigns[account-id]` and `adwords[account-id]`.

The `campaigns` table *should be used by default*, so you can begin by syncing all relevant fields from that table.

The `adwords` table contains four columns that are not in the `campaigns` table:

* `keyword`
* `adContent`
* `adDestinationUrl`
* `adGroup`

Whenever you are interested in performing an analysis that considers these attributes, you must use the `adwords` table. 

>[!IMPORTANT]
>
>This table will exclude rows where all four of these columns are `null`.

Here is a look at the expected schema for both tables:

## `Campaigns` table

The `campaigns` table contains the following columns:

| **Column** | **Description** |
|-----|-----|
| `\_id` | The primary key for the table  |
| `accountId` | The account ID |
| [`adClicks`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&group=adwords&jump=ga_adclicks) | Total number of clicks for the day |
| [`adCost`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&group=adwords&jump=ga_adcost) | Total cost for the campaign for the day |
| [`adwordsCampaignID`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&group=adwords&jump=ga_adwordscampaignid) | [!DNL Adwords] Campaign ID |
| [`campaign`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&group=traffic_sources&jump=ga_campaign) | Campaign name (for example, [utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)) |
| [`date`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&group=time&jump=ga_date) | The date the campaign ran |
| [`impressions`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&group=adwords&jump=ga_impressions) | Number of impressions for the day |
| `profileId` | The profile ID |
| `profileName` | The profile name |
| `\_updated\_at` | The date and time of the last update for this row |

{style="table-layout:auto"}

## AdWords table

The `adwords` table contains the following columns:

| **Column** | **Description** |
|-----|-----|
| `\_id` | The primary key for the table  |
| `accountId` | The account ID |
| [`adClicks`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&group=adwords&jump=ga_adclicks) | Total number of clicks for the day |
| [`adCost`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&group=adwords&jump=ga_adcost) | Total cost for the campaign for the day |
| [`adwordsCampaignID`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&group=adwords&jump=ga_adwordscampaignid) | [!DNL Adwords] Campaign ID |
| [`campaign`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&group=traffic_sources&jump=ga_campaign) | Campaign name (for example, [utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)) |
| [`date`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&group=time&jump=ga_date) | The date the campaign ran |
| [`impressions`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&group=adwords&jump=ga_impressions) | Number of impressions for the day |
| `profileId` | The profile ID |
| `profileName` | The profile name |
| `\_updated\_at` | The date and time of the last update for this row |
| `keyword` | The keyword of the campaign |
| `adContent` | The first line of the text for the online campaign |
| `adDestinationUrl` | The URL to which the [!DNL Adwords] ads referred traffic |
| `adGroup` | The name of the [!DNL Adwords] ad group |

{style="table-layout:auto"}

Using this data, you can start creating [metrics ](../../../data-user/reports/ess-manage-data-metrics.md) and [reports](../../../tutorials/using-visual-report-builder.md) based on spending data and [marry it to your lifetime revenue to calculate ROI](../../analysis/roi-ad-camp.md).

## Consolidated tables

We always recommend creating a `consolidated ad spend` table to combine the data from all of your multiple advertising sources into a single table. This enables you to use a single set of metrics for advertising analysis.

Without a consolidated table, if you build a beautiful dashboard on the `adwords` table, you need to replicate the reporting or create duplicate metrics to compare that data to your [!DNL Facebook Ads] data. Using a consolidated table allows you to seamlessly incorporate [!DNL Facebook Ads] data with your existing [!DNL Adwords] reports. (Do not worry – you have the ability to segment by ad platform as well!)

If you have already synced the fields above, contact us to consolidate your ad spend.

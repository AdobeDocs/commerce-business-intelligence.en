---
title: Expected Facebook Ads data
zendesk_id: 360016504532
---

![](../../../assets/Facebook_Logo.png)

After [you have connected your Facebook Ads account](../integrations/facebook-ads.md), you can use the [Data Warehouse Manager](../data-analyst/data-warehouse-mgr/tour-dwm.md %}#syncing) to easily track relevant data fields for analysis.

In this article, we  give you a brief overview of the tables we recommend you sync to your data warehouse. Note that this isn't an exhaustive list, as there are quite a few subtables. We are only highlighting the core tables.

## Core ad campaign tables

These tables contain data about core ad campaign components.

#### [facebook\_campaigns\_\{account-id}](https://developers.facebook.com/docs/reference/ads-api/adcampaign/)

This table is the core table of campaigns in a Facebook Ads account. Columns include campaign id, name, status (active/paused), objective.

#### [facebook\_adsets\_\{account-id}](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign)

This table records is the core table of Ad Sets in a Facebook Ads account. Columns include the Ad Campaign id/name the Ad Set belongs to, the budgeting, bid type, scheduling and audience targeting information.

#### [facebook\_ads\_\{account-id}](https://developers.facebook.com/docs/reference/ads-api/adgroup/)

This table records all of the ads in a Facebook Ads account. Columns include the ad information including the Ad Set and Ad Campaign it belongs to, the ad bidding, ad targeting and reference to specific creative (image/text) that the ad uses.

#### [facebook\_adcreative\_\{account-id}](https://developers.facebook.com/docs/reference/ads-api/adcreative/)

This table records all of the creatives that are used in Ads. These includes creative name, description and relevant image urls where appropriate.

## Segmented campaign tables

The following tables contain an entry for each campaign/set/ad combination for each day, segmented by dimensions such as age, gender, and country.

#### facebook\_ads\_insights\_\{account-id}

This table includes an entry for each campaign/set/ad combination for each day, along with statistics including impressions, clicks, cost, cpc, cpm, cpp, ctr, reach, social\_reach, and spend.

#### facebook\_ads\_insights\_\{account-id}\_~\_actions

This is a subtable of the `facebook_ads_insights_{account_id}` table. It includes conversion data for actions that happen based on different campaigns.

#### facebook\_ads\_insights\_country\_\{account-id}

This table includes the same information as the `facebook_ads_insights_{account_id}` table and segments it by country.

#### facebook\_ads\_insights\_age\_and\_gender\_\{account-id}

This table includes the same information as the `facebook_ads_insights_{account_id}` table and segments it by age and gender.

### Related

* [Connecting Facebook Ads](../integrations/facebook-ads.md)
* [Reauthenticating integrations](https://support.magento.com/hc/en-us/articles/360016733151-Reauthenticating-integrations)


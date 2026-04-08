---
title: Expected Facebook Ads data
description: Learn a brief overview of the tables that are recommended you sync to your Data Warehouse
exl-id: 0c8b907b-1a98-470b-bb2c-55327e88e502
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/LBpqIMm4nGx-Vu-zxw-iPLgNg1yfDsYi0yDyFHCyxvA
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
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
    internal-label: Insights
---
# Expected [!DNL Facebook Ads] data

After you have [connected your [!DNL Facebook Ads] account](../integrations/facebook-ads.md), you can use the [Data Warehouse Manager](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) to easily track relevant data fields for analysis.

This topic gives you a brief overview of the tables Adobe recommends you sync to your Data Warehouse. This only highlights the core tables, as there are quite a few subtables.

## Core ad campaign tables

These tables contain data about core ad campaign components.

### [`facebook _campaigns_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign-group)

This table is the core table of campaigns in a [!DNL Facebook Ads] account. Columns include `campaign id`, `name`, `status (active/paused)`, `objective`.

### [`facebook _adsets_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign)

This table record is the core table of [!DNL Facebook Ads] Sets in a [!DNL Facebook Ads] account. Columns include the Ad `Campaign id/name` the Ad Set belongs to, the budgeting, bid type, scheduling, and audience-targeting information.

### [`facebook _ads_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/adgroup)

This table records all ads in a [!DNL Facebook Ads] account. Columns include the ad information including the Ad Set and Ad Campaign that it belongs to, the ad bidding, ad targeting, and reference to specific creative (image/text) that the ad uses.

### [`facebook _adcreative_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-creative)

This table records creatives that are used in [!DNL Facebook Ads]. Creatives includes creative name, description, and relevant image urls where appropriate.

## Segmented campaign tables

The following tables contain an entry for each campaign/set/ad combination for each day, segmented by dimensions such as age, gender, and country.

### `facebook _ads insights_ (account-id)`

This table includes an entry for each campaign/set/ad combination for each day, along with statistics including impressions, clicks, cost, cpc, cpm, cpp, ctr, reach, social reach, and spend.

### `facebook _ads insights_ (account-id)_~\_actions`

This is a subtable of the `facebook_ads_insights_{account_id}` table. It includes conversion data for actions that happen based on different campaigns.

### `facebook _ads insights country_ (account-id)`

This table includes the same information as the `facebook_ads_insights_{account_id}` table and segments it by country.

### `facebook ads insights age and gender (account-id)`

This table includes the same information as the `facebook_ads_insights_{account_id}` table and segments it by age and gender.

## Related

* [Connecting [!DNL Facebook Ads]](../integrations/facebook-ads.md)
* [Reauthenticating integrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)

---
title: Replicating Google Analytics channels using acquisition sources
description: Learn how to replicate Google Analytics channels using acquisition sources.
exl-id: e7248fe4-94db-4cdf-8f58-1f65061a207d
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/5UBZqrRg-eiDLvcGe93qEX5KQKWc63eTQOLQ9pnprkI
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
  - id: b23e006f-0a29-4f1d-8fd0-77aa56f3d12b
    internal-label: Data modeling
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
---
# [!DNL Google Analytics] using Acquisition Sources

## What are Channels? {#channels}

Creating custom segments to see how different traffic performs and observe trends is one of the most powerful uses for [!DNL Google Analytics]. One class of segments that exist by default in [!DNL Google Analytics] are `Channels`. Channels are a grouping of common ways that people come to your site.  [!DNL Google Analytics] automatically sorts the many ways that you acquire a user - whether it is social media, pay-per-click, email, or referral links - and bundles them into a bucket, or Channel.

## Why do not I see my `channels` in Commerce Intelligence? {#nochannels}

`Channels` are simple, aggregate buckets of data. To sort your acquisitions into Channel buckets, [!DNL Google] sets distinct rules and definitions using specific parameters: a combination of acquisition [Source](https://support.google.com/analytics/answer/1033173?hl=en) (the origin of your traffic) and acquisition [Medium](https://support.google.com/analytics/answer/6099206?hl=en) (the general category of the source).

While having these buckets can help you make sense of where your traffic is coming from, this data is not tagged by channel but by a combination of Source and Medium. Because [!DNL Google] sends channel information as two separate data points, channel groupings do not automatically show up in [!DNL Commerce Intelligence].

## What are the default channel groupings? How are they created?

By default, [!DNL Google] sets up eight different channels. The rules that determine how channels are created are below.

| **Channel** | **What is it?** | **How is it created?** |
|---|---|---|
| Direct | Anyone who comes directly into your site. | Source = `Direct`<br>AND Medium = `(not set); OR Medium = (none)` |
| Organic Search | Traffic that has been organically ranked in unpaid search engines. | Medium = `organic` |
| Referral | Traffic that comes in from an external link that is not Organic Search or from websites that are not social networks. | Medium = `referral`|
| Paid Search | Traffic that has a UTM Tracking code where the medium is either "cpc", "ppc", or "paidsearch" AND is an ad distribution network that does not match "Content." | Medium = `^(cpc`\|`ppc`\|`paidsearch)$`<br>AND Ad Distribution Network ≠ `Content` |
| Social | Referral traffic that comes from any of approximately 400 social networks and are not tagged as ads. | Social Source referral = `Yes`<br>OR Medium = `^(social`\|`social-network`\|`social-media`\|`sm`\|`social network`\|`social media)$` |
| Email | Traffic from sessions that are tagged with a medium of "email." | UTM Tracking code of Medium = `email` |
| Display | Traffic that has a UTM Tracking code where the medium is either display or cpm. Also includes AdWords interaction where the ad distribution network matches "Content" | Medium = `^(display`\|`cpm`\|`banner)$`<br>OR Ad Distribution Network = `Content`<br>AND Ad Format ≠ `Text` |
| Other | Sessions from other advertising channels (not including Paid Search) that are tagged with a medium of "cpc", "ppc", "cpm, "cpv", "cpa", "cpp", "affiliate". | Medium = `^(cpv`\|`cpa`\|`cpp`\|`content-text)$` |

{style="table-layout:auto"}

## How can I recreate these channel groupings in my Data Warehouse? {#recreate}

Now that you know channels are just combinations of sources and mediums, it is an easy 3-step process to recreate these groupings in your Data Warehouse.

1. **Enable your[!DNL Google ECommerce]integration**

   [When enabled](../importing-data/integrations/google-ecommerce.md), make sure to [sync](tour-dwm.md#syncing) the **medium** and **source** fields in your Data Warehouse. After this is completed, medium and source acquisition data will be brought into your Data Warehouse.

1. **Upload a mapping of Google's channel groupings**

   Adobe Commerce creates a table with the default groupings mapped as a file that you can [download](../../assets/ga-channel-mapping.csv).

   If you are a [!DNL Google Analytics] pro and created your own channels, you want to add your specific rules to the mapping table before uploading the file into [!DNL Commerce Intelligence].

   Bring it into your Data Warehouse as a [File Upload](../importing-data/connecting-data/using-file-uploader.md).

   ![Data Warehouse Manager interface showing primary key settings](../../assets/Setting_Primary_Keys.png)

1. **Establish a relationship between[!DNL Google ECommerce]and Mappings File Upload**

   To establish a relationship between the[!DNL Google ECommerce] and the mapping table, [submit a support request](../../guide-overview.md#Submitting-a-Support-Ticket) to your Data Analyst team and reference this topic. The analyst creates a new calculated column called **Channel** in the ECommerce table. **After a full update cycle**, this column will be ready to use in a `Filter` or `Group by`.

You now have [!DNL Google Analytics Channel] groupings in your Data Warehouse, which means you can analyze your data from a new perspective:

![Segmenting the Number of Orders metric by Channel](../../assets/GA_Channel_Gif.gif)

In this example, you started simple with segmenting the **Number of Orders** metric by **Channel**. Test out your new column and see what trends you can identify in your [!DNL Google Analytics Channel] data!

## Related documentation

* [Using the Report Builder](../../tutorials/using-visual-report-builder.md)
* [Expected[!DNL Google ECommerce]data](../importing-data/integrations/google-ecommerce-data.md)
* [Building[!DNL Google ECommerce]dimensions with order and customer data](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
* [What are your most valuable acquisition sources and channels?](../analysis/most-value-source-channel.md)

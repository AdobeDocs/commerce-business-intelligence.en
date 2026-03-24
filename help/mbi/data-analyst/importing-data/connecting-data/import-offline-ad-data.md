---
title: Import other ad spend data
description: Learn to import offline or other ad spend data into [!DNL Commerce Intelligence].
exl-id: 6f12a397-0927-4e87-95ff-3a55ccc9e14b
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/jx-MMry1-XGeM4htPkH6GC1Et5nYjyD7aWn3p-nmcC8
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
# Import other ad spend data

Uploading your advertising spend data allows you to measure campaign ROI by marrying your advertising cost and the `customer lifetime value (CLV)` of users acquired from your campaigns.

## Uploading advertising cost data

The first step in analyzing ad spend data is getting the data. Since most advertising platforms allow you to export reports, Adobe recommends you export the raw data from your ad platform and directly upload it to [!DNL Commerce Intelligence] without any manipulation. You can perform operations on the data in your Data Warehouse, so there is no need to double your efforts.

After you have exported the ad spend data, use the [`File Upload` feature](../connecting-data/using-file-uploader.md) to bring the data into your Data Warehouse. You can upload new data to the same [!DNL Commerce Intelligence] table over time.

## Offline Sources

In addition to your online campaigns, you may also have advertisements offline, such as on the radio or a billboard. To account for these cases, you can manually upload a spreadsheet with the cost data to [!DNL Commerce Intelligence].

The table structure explored below is recommended when creating a `.csv` file to record ad spend data. A template file is also attached at the bottom of this topic to serve as example. Recommended columns are:

* `ID` - This is a unique identifier for each data row which is used by the database as primary key. This must be different for every row.
* `Date` - This is the date that the campaign ran, in yyyy-mm-dd format.
* `Amount` - This is the amount that you spent on the campaign.
* `campaign` - This is the campaign name. If you are using [!DNL Google Analytics] to track your other ad spend data, it should match the utm\_campaign name.
* `source` -  This is the source name. If you are using [!DNL Google Analytics], this should match the `utm_source` name.
* `other` (Optional) - You may also incorporate additional columns that help you segment campaigns and cost. It can also be a way to summarize several different UTM Campaign names into a single, coherent campaign for tracking purposes. Rather than set this up manually, it might be good to use a V-Lookup to a second sheet to match each Campaign Name to the Other Name and report it here dynamically.

## Related

* [Connect [!DNL AdWords] data](../integrations/google-adwords.md)
* [Increase ROI on advertising campaigns](../../analysis/roi-ad-camp.md)

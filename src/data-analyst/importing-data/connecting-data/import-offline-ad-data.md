---
title: Importing offline / other ad spend data
zendesk_id: 360016506752
---

Uploading your advertising spend data will allow you to measure campaign ROI by marrying your advertising cost and the customer lifetime value (CLV) of users acquired from your campaigns.

## Uploading advertising cost data

The first step in analyzing ad spend data is getting the data. Since most advertising platforms allow you to export reports, we recommend you export the raw data from your ad platform and directly upload it to Magento BI without any manipulation. You can perform operations on the data in your data warehouse, so there is no need to double your efforts.

After you have exported the ad spend data, use [the File Upload feature]({% link data-analyst/importing-data/connecting-data/using-file-uploader.md %}) to bring the data into your data warehouse. You can upload new data to the same Magento BI table over time.

## Offline Sources

In addition to your online campaigns, you may also have advertisements offline, such as on the radio or a billboard. To account for these cases, you can manually upload a spreadsheet with the cost data to Magento BI.

The table structure explored below is recommended when creating a CSV file to record ad spend data. A template file is also attached at the bottom of this article to serve as example. Recommended columns are:

* **ID** - This is a unique identifier for each data row which is used by the database as primary key. This must be different for every row.
* **Date** - This is the date the campaign ran, in yyyy-mm-dd format.
* **Amount** - This is the amount you spent on the campaign.
* **campaign** - This is the campaign name. If you\'re using Google Analytics (GA) to track your other ad spend data, it should match the utm\_campaign name.
* **source** -  This is the source name. If you\'re using GA, this should match the `utm_source` name.
* **other (Optional)** - You may also incorporate additional columns that will help you segment campaigns and cost. It can also be a way to summarize several different UTM Campaign names into a single, coherent campaign for tracking purposes. Rather than set this up manually, it might be good to use a V-Lookup to a second sheet to match each Campaign Name to the Other Name and report it here dynamically.

## Related

* [Connect AdWords data]({% link data-analyst/importing-data/integrations/google-adwords.md %})
* [Increase ROI on advertising campaigns]({% link data-analyst/analysis/roi-ad-camp.md %})

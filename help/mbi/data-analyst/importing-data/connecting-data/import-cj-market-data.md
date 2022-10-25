---
title: Importing CJ Affiliate (Commission Junction) Marketing Data
description: Learn to import CJ Affiliate (Commission Junction) data into [!DNL MBI].L MBI].
---
# Import CJ Affiliate data

To import CJ Affiliate (Commission Junction) data into [!DNL MBI], simply follow the steps below and attach the resulting file to a support ticket. We will setup the data table your account and allow you to continue uploading data independently.

## Export CJ Affiliate Data

1. In your CJ Affiliate account, go to the **Reports** tab.

1. In the _Performance_ tab, select **Report Options**.

1. Set **Performance By** equal to `Program`, **Trend** equal to `Daily`, and **Date Range** equal to the date range being audited.

    ![export-cj-affiliate-data](../../../assets/export-cj-affiliate-data-1.png)<!--{:.zoom}-->

1. Select **Run Report.**

1. In the **File Format** dropdown, select **CSV**.  Click **Download**.

    ![export cj affiliate data](../../../assets/export-an-individual-order-2.jpg)<!--{:.zoom}-->

1. After  you have downloaded the file, you can [upload the file](../connecting-data/using-file-uploader.md) to your [!DNL MBI] data warehouse.

   This creates a new table in your [!DNL MBI] data warehouse that you can continue to upload fresh data into periodically. When uploading the file, be sure to to follow the formatting requirements listed in [Using the File Uploader](../connecting-data/using-file-uploader.md).

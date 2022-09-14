---
title: Importing CJ Affiliate (Commission Junction) Marketing Data
zendesk_id: 360016732671
---

To import CJ Affiliate/Commission Junction data into MBI, simply follow the steps below and attach the resulting file to a support ticket. We will setup the data table your account and allow you to continue uploading data independently.

## Export CJ Affiliate Data

1. In your CJ Affiliate account, go to the **Reports** tab.

1. In the **Performance** tab, select **Report Options**

1. Set **Performance By** equal to `Program`, **Trend** equal to `Daily`, and **Date Range** equal to the date range being audited.

    ![Screen_Shot_2014-02-04_at_3.30.56_PM.png](../../../assets/Screen_Shot_2014-02-04_at_3.30.56_PM.png)<!--{:.zoom}-->

1. Select **Run Report.**

1. In the **File Format** dropdown, select **CSV**.  Click the **Download** button.

    ![Screen_Shot_2014-02-04_at_3.31.27_PM.png](../../../assets/Screen_Shot_2014-02-04_at_3.31.27_PM.png)<!--{:.zoom}-->

1. After  you have downloaded the file, you can [upload the file](../connecting-data/using-file-uploader.md) to your MBI data warehouse.

   This creates a new table in your MBI data warehouse that you can continue to upload fresh data into periodically. When uploading the file, be sure to to follow the formatting requirements listed in [Using the File Uploader](../connecting-data/using-file-uploader.md).

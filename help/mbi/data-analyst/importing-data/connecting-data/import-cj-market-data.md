---
title: Importing CJ Affiliate (Commission Junction) Marketing Data
description: Learn to import CJ Affiliate (Commission Junction) data into [!DNL Commerce Intelligence].L Commerce Intelligence].
exl-id: 1db83f34-15a1-4599-ab0a-65d527ccae01
---
# Import [!DNL CJ Affiliate] data

To import [!DNL CJ Affiliate (Commission Junction)] data into [!DNL Adobe Commerce Intelligence], simply follow the steps below and attach the resulting file to a [support ticket](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html). Adobe will set up the data table your account and allow you to continue uploading data independently.

## Export [!DNL CJ Affiliate] Data

1. In your [!DNL CJ Affiliate] account, go to the `Reports` tab.

1. In the `Performance` tab, select `Report Options`.

1. Set `Performance By` equal to `Program`, `Trend` equal to `Daily`, and `Date Range` equal to the date range being audited.

    ![export-cj-affiliate-data](../../../assets/export-cj-affiliate-data-1.png)<!--{:.zoom}-->

1. Select `Run Report`.

1. In the `File Format` dropdown, select `CSV`.  Click **[!UICONTROL Download]**.

    ![export cj affiliate data](../../../assets/export-an-individual-order-2.jpg)<!--{:.zoom}-->

1. After  you have downloaded the file, you can [upload the file](../connecting-data/using-file-uploader.md) to your [!DNL Commerce Intelligence] Data Warehouse.

   This creates a table in your [!DNL Commerce Intelligence] Data Warehouse that you can continue to upload fresh data into periodically. When uploading the file, follow the formatting requirements listed in [Using the File Uploader](../connecting-data/using-file-uploader.md).

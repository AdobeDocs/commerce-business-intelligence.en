---
title: Importing CJ Affiliate (Commission Junction) Marketing Data
description: Learn to import CJ Affiliate (Commission Junction) data into [!DNL Commerce Intelligence].L Commerce Intelligence].
exl-id: 1db83f34-15a1-4599-ab0a-65d527ccae01
TQID: https://experienceleague.adobe.com/tZ2fzAKou0fBmkmKD5zdLFBNCSiAGpT3GNgkHp9ptx4
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
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

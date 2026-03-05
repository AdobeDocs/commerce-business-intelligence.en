---
title: Importing Linkshare data
description: Learn to import Linkshare data into [!DNL Commerce Intelligence].
exl-id: 1c2025a6-746c-4929-bbb1-62af1afcbc49
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/TsQYXEwH-8m1rpKg6It8wa-B2eQH0oqDkLcgx-tRBWU
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
# Import [!DNL Linkshare] data

To bring your [!DNL Linkshare] data into [!DNL Adobe Commerce Intelligence], you need to do two things:

1. [Export the Linkshare data in `.csv` format](#export)
1. [Upload the spreadsheet into [!DNL Commerce Intelligence]](../connecting-data/using-file-uploader.md)

## Export data from Linkshare {#export}

1. In your [!DNL Linkshare] account, go to **[!UICONTROL Reports** > **Run Reports].**

1. In the `Report` dropdown, select **[!UICONTROL Sales & Activity Report]**.

1. Leave all other dropdown options as the default selection.

1. In the `Date Range` dropdown, select whichever option (`Sun - Sat`, `Mon - Sun`) matches with your `Start of Week` settings in [!DNL Commerce Intelligence].

1. Clear the `Compare Year-Over-Year Data` checkbox.

1. Under `Data Type`, select `Transaction Date`.

    ![importing\_linkshare\_data.png](../../../assets/importing_linkshare_data.png)

1. Click **[!UICONTROL View Report]**.

1. Click **[!UICONTROL Download]**.

   At this point, a `.csv` file  and downloaded.

After the file is downloaded, you can upload it to [!DNL Commerce Intelligence] using the [`File Upload` feature](../connecting-data/using-file-uploader.md).

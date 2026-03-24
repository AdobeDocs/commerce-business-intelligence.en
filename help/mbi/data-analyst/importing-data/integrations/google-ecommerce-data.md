---
title: Expected[!DNL Google ECommerce]data
description: Learn what types of data are shared with Google ECommerce.
exl-id: 8e5d8863-f003-4c38-95c5-660bcbff48da
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/tGcSyz6DHcusK-RomMkRZoyY7acXb0dmXlHcc5pW7cg
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
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
---
# Expected [!DNL Google ECommerce] data

After your [!DNL Google ECommerce] account is successfully connected to [!DNL Commerce Intelligence], the system will start importing data into a table titled `ecommerce`. This table records a data row for each transaction. This includes the following order-level data columns:

| Column Name | Description |
|-----|-----|
| `\_id` | This column is the primary key. |
| `accountId` | This column contains the account ID associated with your [!DNL Google Analytics] eCommerce account. |
| `profileName` | This column contains your [!DNL Google Analytics] profile name. |
| `profileId` | This column contains your [!DNL Google Analytics] profile ID. |
| `socialNetwork` | This column contains the name of the social network (for example, [!DNL Facebook], or [!DNL YouTube]) |
| `campaign` | This column contains the campaign name (for example, [`utm\_campaign`](https://support.google.com/analytics/answer/1033867?hl=en)). |
| `medium` | This column contains the medium name (for example, [`utm\_medium`](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `source` | This column contains the source name. (for example, [`utm\_source`](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `keyword` | This column contains the keyword description (for example, [`utm\_term`](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `transactionId` | This column contains the order ID. This is used to join the referral data back to your orders data. |
| `updated\_at` | This column contains the last time that the data row was updated. |

{style="table-layout:auto"}

---
title: Expected[!DNL Google ECommerce]data
description: Learn what types of data are shared with Google ECommerce.
exl-id: 8e5d8863-f003-4c38-95c5-660bcbff48da
---
# Expected[!DNL Google ECommerce] data

After your [!DNL Google ECommerce] account is successfully connected to [!DNL MBI], the system will start importing data into a table titled `ecommerce`. This table records a data row for each transaction. This includes the following order-level data columns:

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

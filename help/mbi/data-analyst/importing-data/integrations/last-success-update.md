---
title: Understand Results Between Database and SQL Editor
description: Learn to understand results between database and SQL editor.
exl-id: f31f3eef-791a-4984-901e-bc10554031bd
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/pScH-yKW8hbSNZzsJ537CN7rxhcuygaLmCu3fdVaYgk
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
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
---
# Database Results vs [!DNL SQL Editor] Results

You may be curious what the `Last successful update began` field is inside your `Integrations` page:

![Last_successful_update.png](../../../assets/Last_successful_update.png)

## Understand the `timestamp` field

It shows the start `timestamp` (in the timezone set on your account) of the _last successful update cycle_ on your account.

-  If any of the synced tables encountered an issue during the last update cycle, this timestamp is *not updated*.
-  Hence, there may be cases when reports have been updated with fresh data, but the *Last successful update began* is still lagging.

## Identify the "real" last data point

The latest data point for a particular integration is determined by the `Last Data Point Received` timestamp located on the right of each integration. That timestamp refers to the last point at which your Data Warehouse successfully received data points from that source, whether it be a database, API, or third-party integration.

To check for freshness of data from *specific tables*, Adobe recommends creating a quick [[!DNL SQL] report](../../dev-reports/sql-rpt-bldr.md) that performs a `MAX(timestamp)` on the most important table on your account. Comparing this timestamp to the `Last Data Point` indicates whether the issue affected the entire account or a subset of the tables. Adobe recommends doing this for three to four important, commonly used tables.

-  If the `MAX(timestamp)` values are more recent than `Last Data Point Received`, it means that a subset of the tables were affected, but the overall account's update cycle is stable.
-  If the `MAX(timestamp)` values are equal to or before `Last Data Point Received`, it means that the account's update cycle was affected. In this situation, [submit a support ticket](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

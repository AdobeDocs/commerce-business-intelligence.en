---
title: Differences Between SQL and Data Warehouse Manager
description: Learn the differences between SQL and Data Warehouse Manager.
exl-id: 31dd7a04-5c03-4399-b67e-f51703eb9fea
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, SQL Report Builder, Reports
TQID: https://experienceleague.adobe.com/aWLLAi9e-A6Di7AGujRNd79W7GqSRo5yIgmQRZAHOEQ
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
---
# Differences Between [!DNL SQL] and [!DNL Data Warehouse Manager]

There are two key differences between columns created in the [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) and those created using the [[!DNL Data Warehouse Manager]](../data-warehouse-mgr/creating-calculated-columns.md). One is the dependency on update cycles, and the other is how columns are saved in your account.

## Columns in the [!DNL SQL Report Builder]

Columns are not dependent on update cycles, so you no longer have to wait for one to complete before you can iterate on your column. If you make a mistake, it only takes a few keystrokes to correct it - no more waiting for two updates to wrap up before you can get back to work.

>[!IMPORTANT]
>
>The columns you create using the [!DNL SQL] editor are not saved to your Data Warehouse. You always have access to the query containing the column, but if you want to use the column in more than one report, you have to recreate it in the query for each report. This means that columns created using the [!DNL SQL] editor cannot be used in the traditional [!DNL Report Builder].

## Columns in the Data Warehouse Manager

Columns depend update cycles, so a full cycle must complete before they can be edited. These columns are saved to the Data Warehouse Manager and can be used in the traditional [!DNL Report Builder] or [!DNL SQL Report Builder].

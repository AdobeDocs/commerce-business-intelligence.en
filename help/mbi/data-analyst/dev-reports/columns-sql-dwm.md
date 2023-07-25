---
title: Differences Between SQL and Data Warehouse Manager
description: Learn the differences between SQL and Data Warehouse Manager.
exl-id: 31dd7a04-5c03-4399-b67e-f51703eb9fea
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, SQL Report Builder, Reports
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

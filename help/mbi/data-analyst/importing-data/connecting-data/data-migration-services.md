---
title: Data migration services
description: Learn everything that you need to submit a request and get started on the migration.
exl-id: 105cd003-98ef-4358-80b9-b3190c2c57b7
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/q8FzCjuqcQC57WLd0201CV46es2CrbAjZx9FGFX-RFw
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
  - id: f42e0a1a-0d79-488d-a83f-f2c30672b137
    internal-label: Reporting
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
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
    internal-label: Reporting
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
---
# Data Migration

Migrating to a new database schema, server, or reporting database does not have to be stressful. The [[!DNL Adobe] Services team](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) offers migration assistance.

To ensure that your transition is as smooth as possible, you should be as detailed as possible when submitting your migration request. This topic has everything that you need to submit a request and get started on the migration. Providing us with a comprehensive picture of your needs guarantee that your project is scoped properly and that the estimate is accurate.

## Getting started {#started}

Before getting started, you must know the answers to these questions:

* **Is the new database on a new server?** Before submitting a request, update your data connection's settings under **[!UICONTROL Manage Data** > **Connections]**. If you need a refresher on how to do this, go to the [`Integrations`](../integrations/integrations.md) section and find the instructions for the type of database you are using.

* **Does your all historical data exist in the new database or does it need to be migrated?** You can consolidate the historical and new data during the migration process. Even if you do not need a consolidation, let us know in your request.

After you have the answers to the above, you need to know the type of migration. Will the new database have the [`same`](#sameschema) schema, or will it have a [`different`](#newschema) schema? In the discussions below, you find detailed instructions for each migration type.

## Migrating to a new database with the same schema {#sameschema}

When submitting the request, let us know that the database schema is not changing and that the connection is already set up in [!DNL Adobe Commerce Intelligence].

If the database has a new name, include it in the request so your dashboards can be properly migrated.

If the database name is not changing, the migration is complete. Dashboards and reports will refresh after the next full update is completed.

## Migrating to a new database with a different schema {#newschema}

>[!IMPORTANT]
>
>If certain data columns do not have equivalent columns in the new database, there is a chance that certain analyses may be lost in the process.

To successfully complete this type of migration, existing data columns have to be matched with their equivalents in the new database. This is not mandatory, but performing the matching for us helps speed up the turn-around time of your request and lower the price of the migration.

If you feel comfortable doing the matching yourself, follow these instructions and attach the finished spreadsheet to your request:

1. Review all the tables and columns currently syncing to your Data Warehouse (**[!UICONTROL Manage Data** > **Data Warehouse]**).

1. In a spreadsheet, create a tab for every table to be migrated to the new database.

1. In each tab, create a column for all the existing columns that need to be migrated. Adobe recommends naming it something like `Existing column name`.

1. You also need to make another column for the column equivalents in the new database in each tab of the spreadsheet. Adobe recommends naming the column something like `New column name`.

1. Enter the existing columns and their equivalents. If an existing column does not have a new equivalent, enter `N/A`.

    Also, if there is a new way to calculate the same information in the new database, enter it in the [`New column name`] column.

Here is a look at an example:

![Migration spreadsheet template with database schema and table structure](../../../assets/Migration_Spreadsheet.png)

>[!NOTE]
>
>If certain data columns do not have equivalent columns in the new database, there is a chance that certain analyses may be lost in the process.

## How do I submit a request? {#submitreq}

You can reach out to us by [submitting a support request](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

If you followed the steps in the previous section for creating the column-matching spreadsheet, do not forget to attach it.

## What is next? {#wrapup}

Determining the scope of the project takes some collaboration between you and the analyst from the Commerce Services team performing the migration. The complexity of the changes and the responsiveness of you and the analyst directly impacts the amount of time the migration can take. After you nail down the details, a timeline will be established and sent to you with a statement of work.

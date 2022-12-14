---
title: Data migration services
description: Learn everything you need to submit a request and get started on the migration.
exl-id: 105cd003-98ef-4358-80b9-b3190c2c57b7
---
# Data Migration

Migrating to a new database schema, server, or reporting database does not have to be stressful. Our **[!DNL Magento Services - Analytics]** team offers migration assistance - we do all the heavy lifting so you do not have to.

To ensure your transition is as smooth as possible, we ask that you be as detailed as possible when submitting your migration request. In this article is everything you need to submit a request and get started on the migration. Providing us with a comprehensive picture of your needs will guarantee that your project is scoped properly and that the estimate is accurate.

## Getting started {#started}

Before we dive in, you should know the answers to these questions:

* **Is the new database on a new server?** Before submitting a request, update your data connection's settings under **[!UICONTROL Manage Data** > **Connections]**. If you need a refresher on how to do this, go to the [`Integrations`](../integrations/integrations.md) section and find the instructions for the type of database you are using.
* **Does your all historical data exist in the new database or does it need to be migrated?** We can consolidate the historical and new data during the migration process. Even if you do not need a consolidation, we ask that you let us know in your request.

After you have the answers to the above, we will need to know the type of migration: will the new database have the [`same`](#sameschema) schema, or will it have a [`different`](#newschema) schema? In the sections below, you will find detailed instructions for each migration type.

## Migrating to a new database with the same schema {#sameschema}

When submitting the request, let us know that the database schema is not changing and that the connection is already set up in [!DNL MBI].

If the database has a new name, include it in the request so your dashboards can be properly migrated.

If the database name is not changing, the migration is complete. Dashboards and reports will refresh after the next full update is completed. We ask that you still contact us so that we can stay ahead of any problems that might result from the migration.

## Migrating to a new database with a different schema {#newschema}

>[!IMPORTANT]
>
>If certain data columns do not have equivalent columns in the new database, there is a chance that certain analyses will be lost in the process.

To successfully complete this type of migration, existing data columns have to be matched with their equivalents in the new database. This is not mandatory for you to do, but performing the matching for us will help speed up the turnaround time of your request and lower the price of the migration.

If you feel comfortable doing the matching yourself, follow these instructions and attach the finished spreadsheet to your request:

1. Review all the tables and columns currently syncing to your Data Warehouse (**[!UICONTROL Manage Data** > **Data Warehouse]**).
1. In a spreadsheet, create a tab for every table to be migrated to the new database.
1. In each tab, create a column for all the existing columns that need to be migrated. We recommend naming it something like `Existing column name`.
1. You also need to make another column for the column equivalents in the new database in each tab of the spreadsheet. We recommend naming the column something like `New column name`.
1. Enter the existing columns and their equivalents. If an existing column does not have a new equivalent, just enter `N/A`.

    Additionally, if there is a new way to calculate the same information in the new database, enter it in the [`New column name`] column.

Here is a look at an example:

![](../../../assets/Migration_Spreadsheet.png)

>[!NOTE]
>
>If certain data columns do not have equivalent columns in the new database, there is a chance that certain analyses will be lost in the process.

## How do I submit a request? {#submitreq}

You can reach out to us by [submitting a support request](../../../guide-overview.md).

If you followed the steps in the previous section for creating the column matching spreadsheet, do not forget to attach it.

## What is next? {#wrapup}

Determining the scope of the project will take some collaboration between you and the analyst from the [!UICONTROL Magento] Services team performing the migration. The complexity of the changes and the responsiveness of you and the analyst directly impacts the amount of time the migration can take. After we nail down the details, a timeline will be established and sent to you with a statement of work.

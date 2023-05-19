---
title: Connect Your Data
description: Learn how to browse the tables available for syncing in the Data Warehouse Manager.
exl-id: 94beba8b-6a86-4af9-87fb-96b1cf8f8fa2
---
# Connect your Data

In [!DNL Adobe Commerce Intelligence], data sources are called `integrations`. After an `integration` is successfully connected, you will be able to browse the tables available for syncing in the Data Warehouse Manager.

Integrations are added and managed using the `Connections` page, which can be accessed by clicking **[!UICONTROL Manage Data** > **Connections]**. Here, you see:
 
* a list of all the integrations connected to your account

* the integration type

* status ([!DNL Google Analytics] and [!DNL Data Import API] connections have blank status fields)

* the last time a connection test (`Last Connection Started` column) was performed

![Data\_Sources\_Table.png](../../../assets/Data_Sources_Table.png)

## Types of Integrations

There are four ways to get your data into [!DNL Commerce Intelligence]: connect a database, connect a SaaS integration, upload a `.csv` file, or use the Adobe API.

## Database Integrations

![Database\_icons.jpg](../../../assets/Database_icons.jpg)

[!DNL Commerce Intelligence] supports SQL-based and NoSQL databases such as [MySQL](../../importing-data/integrations/mysql-via-ssh-tunnel.md), [Microsoft SQL](../integrations/microsoft-sql-server.md), [MongoDB](../integrations/mongodb-via-ssh-tunnel.md), and [PostgreSQL](../integrations/postgresql.md).

While you can directly connect your database to [!DNL Commerce Intelligence] using database credentials, Adobe recommends you use a proven encryption method like an SSH tunnel. This ensures that your data stays safe and secure as it makes its way into your Data Warehouse.

Depending on the connection method and type of database, some technical expertise might be required to complete the setup.

## `SaaS` Integrations

![](../../../assets/SaaS_icons.jpg)spree-commerce-logo.png

`SaaS` integrations are services like [[!DNL Google Adwords]](../integrations/google-adwords.md), [[!DNL Salesforce]](../integrations/salesforce.md), and [[!DNL Zendesk]](../integrations/zendesk.md). Because third-party data lives on the vendor's server, you cannot directly access it like you can with the data in your database.

Usually, setting up an integration in [!DNL Commerce Intelligence] is as easy as simply entering your account credentials. Some services might require an API key to complete the authorization. Check out the [integrations section](../integrations/integrations.md) for instructions on generating any credentials you need.

## File Upload

Not sure how to get data from a supplementary source into your Data Warehouse? [Using the `File Upload` feature](../connecting-data/using-file-uploader.md) is a good way to pull in data that you do not need for everyday decision making. Following the formatting rules, you can quickly upload `.csv` files into your Data Warehouse and join them with other data sources.

## [!DNL Commerce Intelligence] `Import API`

If you would rather automate the retrieval of data from one of your own sources, you can use the [!DNL Commerce Intelligence] `Import API`. Basically, if it is not in a database or a `SaaS` integration, the `Import API` function is your best bet.

Using the API requires a bit of technical expertise - someone who is comfortable with writing and maintaining a small Ruby or PHP script is more than qualified.

To learn more about getting started with the `Import API`, check out the [Developer site](https://developer.adobe.com/commerce/services/reporting/) and [how to generate an API key](https://developer.adobe.com/commerce/services/reporting/import-api/).

## Add an Integration

To add an integration, click **[!UICONTROL Manage Data** > **Connections]** and then click **[!UICONTROL Add a New Data Source]**. Click the icon of the integration that you want to add and follow the instructions in help topics to set things up:

* [Integration FAQ](https://support.magento.com/hc/en-us/sections/360003161871-Integration-FAQ)
* [Available `SaaS` and `database` integrations](../integrations/integrations.md)
* [Consolidating your tables](../../../best-practices/consolidating-your-tables.md)
* [Restricting access to your database](../../../administrator/account-management/restrict-db-access.md)

**Not seeing an integration you want?** Some integrations must be activated for them to be visible in your account. If you are looking for something like [!DNL Facebook] but it is not listed, [submit a support ticket](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

**If you see an error status for an integration**, check out the [Troubleshooting section](https://support.magento.com/hc/en-us/sections/360003078151) for help.

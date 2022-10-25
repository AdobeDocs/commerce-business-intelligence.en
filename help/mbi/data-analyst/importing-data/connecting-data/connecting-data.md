---
title: Connect Your Data
description: Learn how to browse the tables available for syncing in the Data Warehouse Manager.
---
# Connect your Data

In [!DNL MBI], data sources are called **integrations**. After an integration is successfully connected, you will be able to browse the tables available for syncing in the Data Warehouse Manager.

Integrations are added and managed using the **Connections** page, which can be accessed by clicking **Manage Data > Connections.** Here, you'll see a list of all the integrations connected to your account, the integration type, status ("Google Analytics" and "Data Import API" connections will have blank status fields), and the last time a connection test (Last Connection Started column) was performed.

![Data\_Sources\_Table.png](../../../assets/Data_Sources_Table.png)

## Types of Integrations

There are four ways to get your data into MBI: connect a database, connect a SaaS integration, upload a CSV file, or use our API.

## Database Integrations

![Database\_icons.jpg](../../../assets/Database_icons.jpg)

MBI supports SQL-based and NoSQL databases such as [MySQL](../../importing-data/integrations/mysql-via-ssh-tunnel.md), [Microsoft SQL](../integrations/microsoft-sql-server.md), [MongoDB](../integrations/mongodb-via-ssh-tunnel.md), and [PostgreSQL](../integrations/postgresql.md).

While you can directly connect your database to [!DNL MBI] using database credentials, **we recommend you use a proven encryption method like an SSH tunnel**. This will ensure that your data stays safe and secure as it makes its way into your data warehouse.

Depending on the connection method and type of database, some tech expertise might be required to complete the setup.

## SaaS Integrations

![](../../../assets/SaaS_icons.jpg)

SaaS integrations are services like [Google Adwords](../integrations/google-adwords.md), [Salesforce](../integrations/salesforce.md), and [Zendesk](../integrations/zendesk.md). It is important to note that because third-party data lives on the vendor's server, you cannot directly access it like you can with the data in a database.

In most cases, setting up an integration in [!DNL MBI] is as easy as simply entering your account credentials. Some services might require an API key to complete the authorization - check out the [integrations section](../integrations/integrations.md) for instructions on generating any credentials you need.

## File Upload

Not sure how to get data from a supplementary source into your data warehouse? [Using the File Upload feature](../connecting-data/using-file-uploader.md) is a good way to pull in data that you do not need for everyday decision making. Following our formatting rules, you can quickly upload CSV files into your data warehouse and join them with other data sources.

## [!DNL MBI] Import API

If you would rather automate the retrieval of data from one of your own sources, you can use the [!DNL MBI] Import API. **Basically: if it is not in a database or a SaaS integration**, the Import API is your best bet.

Using the API requires a bit of technical expertise - someone who is comfortable with writing and maintaining a small Ruby or PHP script will be more than qualified.

To learn more about getting started with the Import API, check out the [Developer site](https://devdocs.magento.com/mbi/docs/getting-started.html) and [how to generate an API key](https://devdocs.magento.com/mbi/docs/import-api.html).

## Add an Integration

To add an integration, click **Manage Data > Connections** and then click **Add a New Data Source**. Click the icon of the integration you want to add and follow the instructions in our help articles to set things up:

* [Integration FAQ](https://support.magento.com/hc/en-us/sections/360003161871-Integration-FAQ)
* [Available SaaS and database integrations](../integrations/integrations.md)
* [Consolidating your tables](../../../best-practices/consolidating-your-tables.md)
* [Restricting access to your database](../../../administrator/account-management/restrict-db-access.md)

**Not seeing an integration you want?** Some integrations have to be activated for them to be visible in your account. If you are looking for something - for example, Facebook - but it is not listed, [submit a support ticket](../../../getting-started/support.md).

**If you see an error status for an integration**, do not panic - check out the [Troubleshooting section](https://support.magento.com/hc/en-us/sections/360003078151) for help.

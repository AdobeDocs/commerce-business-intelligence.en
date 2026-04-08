---
title: Connect Your Data
description: Learn how to browse the tables available for syncing in the Data Warehouse Manager.
exl-id: 94beba8b-6a86-4af9-87fb-96b1cf8f8fa2
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration
TQID: https://experienceleague.adobe.com/WwUCbK9dC39RSVL8Nf0PdL10wAdxje-9deR20JScqj0
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
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

![SaaS integration icons showing various supported platforms](../../../assets/SaaS_icons.jpg)spree-commerce-logo.png

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

## Monitor update health (optional)

After you connect sources, you may want to automate a basic health check to confirm that full updates are completing. Use the [Update Cycle Status API](https://developer.adobe.com/commerce/services/reporting/update-cycle-status-api/) in the developer documentation to fetch the most recent completed update cycle for your client and display it in internal dashboards or alerts.

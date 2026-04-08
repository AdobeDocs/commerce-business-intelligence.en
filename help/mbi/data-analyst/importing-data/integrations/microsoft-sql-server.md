---
title: Connect Microsoft SQL Server
description: Learn how to connect your Microsoft SQL database to [!DNL Commerce Intelligence] in a four-step process.
exl-id: 7f49d1dc-8fbb-4a8c-9d07-9a8195c266f5
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export, SQL Report Builder
TQID: https://experienceleague.adobe.com/mJFBPJE334m7V8klJk-1xKAfsU4u4ObcwWDZzylJohM
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
# Connect [!DNL Microsoft SQL] Server

>[!NOTE]
>
>Requires [Admin permissions](../../../administrator/user-management/user-management.md).

![Microsoft SQL Server logo](../../../assets/MicrosoftSQLServer-logo.png)

This topic explains how to connect your [!DNL Microsoft SQL] database to [!DNL Commerce Intelligence] in a four-step process. This process requires some technical expertise related to server connections and SQL, and may require support from developers on your team.

[!DNL Commerce Intelligence] supports [!DNL Amazon RDS], [!DNL EC2], [!DNL Microsoft SQL Azure], and most other cloud server providers. If you have a question on your particular host, [submit a support ticket](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) asking us to provide this information.

Your system needs to run SELECT queries on your database. This is initially done to get a snapshot of your database structure and then regularly overtime to keep your data up to date. Your updates are incremental, and Adobe restrict update frequency and time to prevent any unwanted load on your server.

The best way to do this is for us to connect to your database server over TCP/IP. Create a user for us that can only run SELECT queries (and, optionally, can only select data from the tables you specify). This must be done for each of your servers that you are connecting to [!DNL Commerce Intelligence].

## Connecting `Microsoft SQL` to [!DNL Commerce Intelligence]:

1. Make sure that your server allows connections over TCP/IP and mixed mode authentication.

1. Make sure that your firewall allows your server's dedicated IP to connect.

   You can find the IP address that is used to connect to your server on the connections section of your `Settings` page.

1. Create a user to log into your database server. You have two options; either via `UI` or via a `query`:
    * `UI`
    * `Query`

1. Input the server IP address, username, and password in [!DNL Commerce Intelligence] under **[!UICONTROL Manage Data** > **Connections]**.

    ![Manage Data connections page showing database integrations](../../../assets/manage-data-connections.png)

1. Click **[!UICONTROL Add a Data Source]**.

1. Select to connect a `Microsoft SQL` database and enter your credentials in the fields on the new `Connections` page.

   If you are using `Windows Azure`, you must specify a database name as well.

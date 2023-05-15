---
title: Connect Microsoft&reg;&reg; SQL Server
description: Learn how to connect your Microsoft&reg; SQL database to [!DNL Commerce Intelligence] in a four-step process.
exl-id: 7f49d1dc-8fbb-4a8c-9d07-9a8195c266f5
---
# Connect Microsoft&reg; SQL Server

>[!NOTE]
>
>Requires [Admin permissions](../../../administrator/user-management/user-management.md).

![](../../../assets/MicrosoftSQLServer-logo.png)

This topic explains how to connect your `Microsoft SQL` database to [!DNL Commerce Intelligence] in a four-step process. This process requires some technical expertise related to server connections and SQL, and may require support from developers on your team.

Commerce Intelligence supports [!DNL Amazon RDS], [!DNL EC2], [!DNL Microsoft&reg;; SQL Azure], and most other cloud server providers. If you have a question on your particular host, [submit a support ticket](../../../guide-overview.md) asking us to provide this information.

Your system needs to run SELECT queries on your database. This is initially done to get a snapshot of your database structure and then regularly overtime to keep your data up to date. Your updates are incremental, and Adobe restrict update frequency and time to prevent any unwanted load on your server.

The best way to do this is for us to connect to your database server over TCP/IP. Create a user for us that can only run SELECT queries (and, optionally, can only select data from the tables you specify). This must be done for each of your servers that you are connecting to [!DNL Commerce Intelligence].

## Connecting `Microsoft SQL` to [!DNL Commerce Intelligence]:

1. Make sure that your server allows connections over TCP/IP and mixed mode authentication.

1. Make sure that your firewall allows your server's dedicated IP to connect.

   You can find the IP address that is used to connect to your server on the connections section of your `Settings` page.

1. Create a user that to use to log into your database server. You have two options; either via `UI` or via a `query`:
    * `UI`
    * [`Query`](http://sqlserverplanet.com/security/add-user) (second example)

1. Input the server IP address, username, and password in [!DNL Commerce Intelligence] under **[!UICONTROL Manage Data** > **Connections]**.

    ![](../../../assets/manage-data-connections.png)

1. Click **[!UICONTROL Add a Data Source]**.

1. Select to connect a `Microsoft SQL` database and enter your credentials in the fields on the new `Connections` page.

   If you are using `Windows Azure`, you must specify a database name as well.

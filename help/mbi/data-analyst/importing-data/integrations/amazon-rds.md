---
title: Connect Amazon RDS
description: Learn the steps for connecting your RDS instance.
exl-id: 02ad29c8-84d6-4b49-9ac1-e5f4feaa7fda
---
# Connect [!DNL Amazon RDS]

[!DNL Amazon Relational Database Services (RDS)] is a managed database service that runs on database engines that you are probably already familiar with:

* [[!DNL MySQL]](../integrations/mysql-via-a-direct-connection.md)
* [[!DNL Microsoft SQL]](../integrations/microsoft-sql-server.md)
* [[!DNL PostgreSQ]](../integrations/postgresql.md).

The steps for connecting your [!DNL RDS] instance vary, depending on the type of database you are using and whether you are using an encrypted connection (like an [`SSH tunnel for MySQL`](../integrations/mysql-via-ssh-tunnel.md)), but here are the basics.

## Authorize [!DNL Commerce Intelligence] to access your database

On the credentials page (**[!UICONTROL Manage Data** > **Integrations]**) for each database, you see a box containing the IP addresses you must authorize to connect R[!DNL RDS] to [!DNL Commerce Intelligence]: `54.88.76.97` and `34.250.211.151`. Here is a look at the `MySQL credentials` page, where you highlighted the IP address box:

![](../../../assets/RDS_IP.png)

For [!DNL Commerce Intelligence] to successfully connect with your [!DNL RDS] instance, you must add these IP addresses to the appropriate database security group via the AWS management console. These IP addresses can be added to an existing group or you can create a one - the important thing is that the group is authorized to access the instance you want to connect to [!DNL Commerce Intelligence].

When adding the [!DNL Commerce Intelligence] IP addresses, make sure you add a `/32` to the end of the address to indicate to [!DNL Amazon] that it is an exact IP address. Do not worry; the AWS interface makes it clear that this is required.

## Create a `Linux` user for [!DNL Commerce Intelligence] {#linux}

>[!NOTE]
>
>This step is only required if you are using an encrypted connection. For instructions on how to do this, refer to the setup topic for the database you are using (ex: MySQL). The `Linux` user allows us to create an `SSH tunnel`, which is the safest method of sending data over the internet.

## Create a database user for Commerce Intelligence

This is the part of the process where, depending on the database you are using, the steps vary. The idea is the same, though, you create a user for [!DNL Commerce Intelligence] which is used to access your database. Instructions for creating a database [!DNL Commerce Intelligence] user can be found in the setup topic for the database you are using.

## Enter connection info into Commerce Intelligence

After you have granted [!DNL Commerce Intelligence] access to your instance and created a user for us, the last thing you need to do is enter the connection info into [!DNL Commerce Intelligence].

The credential pages for `MySQL`, `Microsoft SQL`, and `PostgreSQL` are accessed via the `Integrations` page (**[!UICONTROL Manage Data** > **Integrations]**) by clicking **[!UICONTROL Add Integration]**. When the list of integrations displays, click the icon for the database you are using to go to the credentials page. If you do not currently have access to the integration you need, contact your Adobe Account Team.

To finish creating the connection, you need the following info:

*  The public address of your RDS instance: This can be found in the [!DNL AWS] management console.
*  The port your database instance uses: Some databases have a default port, which automatically populates the `Port` field. This info can also be found in the setup documentation for the database.
*  The username and password of the user you created for [!DNL Commerce Intelligence].

If you are using an encrypted connection, change the `Encrypted` toggle on the database credentials page to `Yes`. This displays an extra form for setting up the encryption:

![](../../../assets/sql-integration-encrypted-yes.png)



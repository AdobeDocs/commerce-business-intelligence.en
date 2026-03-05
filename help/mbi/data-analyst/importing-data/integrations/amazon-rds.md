---
title: Connect Amazon RDS
description: Learn the steps for connecting your RDS instance.
exl-id: 02ad29c8-84d6-4b49-9ac1-e5f4feaa7fda
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/KAjnETtFvi9EHUDY8SJ-TSEhP3zooQel5ZlN-E3QxIg
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
    internal-label: Security
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
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
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
---
# Connect [!DNL Amazon RDS]

[!DNL Amazon Relational Database Services (RDS)] is a managed database service that runs on database engines that you are probably already familiar with:

* [[!DNL MySQL]](../integrations/mysql-via-a-direct-connection.md)
* [[!DNL Microsoft SQL]](../integrations/microsoft-sql-server.md)
* [[!DNL PostgreSQL]](../integrations/postgresql.md)

The steps for connecting your [!DNL RDS] instance vary, depending on the type of database you are using and whether you are using an encrypted connection (like an [`SSH tunnel for MySQL`](../integrations/mysql-via-ssh-tunnel.md)), but here are the basics.

## Authorize [!DNL Commerce Intelligence] to access your database

On the credentials page (**[!UICONTROL Manage Data** > **Integrations]**) for each database, you see a box containing the IP addresses you must authorize to connect R[!DNL RDS] to [!DNL Commerce Intelligence]: `54.88.76.97` and `34.250.211.151`. Here is a look at the `MySQL credentials` page, where you highlighted the IP address box:

![Amazon RDS security group settings showing IP address configuration](../../../assets/RDS_IP.png)

For [!DNL Commerce Intelligence] to successfully connect with your [!DNL RDS] instance, you must add these IP addresses to the appropriate database security group via the AWS management console. These IP addresses can be added to an existing group or you can create a one - the important thing is that the group is authorized to access the instance you want to connect to [!DNL Commerce Intelligence].

When adding the [!DNL Commerce Intelligence] IP addresses, make sure you add a `/32` to the end of the address to indicate to [!DNL Amazon] that it is an exact IP address. Do not worry; the AWS interface makes it clear that this is required.

## Create a `Linux` user for [!DNL Commerce Intelligence] {#linux}

>[!NOTE]
>
>This step is only required if you are using an encrypted connection. For instructions on how to do this, refer to the setup topic for the database you are using (ex: MySQL). The `Linux` user allows us to create an `SSH tunnel`, which is the safest method of sending data over the internet.

## Create a database user for [!DNL Commerce Intelligence]

This is the part of the process where, depending on the database you are using, the steps vary. The idea is the same, though, you create a user for [!DNL Commerce Intelligence] which is used to access your database. Instructions for creating a database [!DNL Commerce Intelligence] user can be found in the setup topic for the database you are using.

## Enter connection info into [!DNL Commerce Intelligence]

After you have granted [!DNL Commerce Intelligence] access to your instance and created a user for us, the last thing you need to do is enter the connection info into [!DNL Commerce Intelligence].

The credential pages for `MySQL`, `Microsoft SQL`, and `PostgreSQL` are accessed via the `Integrations` page (**[!UICONTROL Manage Data** > **Integrations]**) by clicking **[!UICONTROL Add Integration]**. When the list of integrations displays, click the icon for the database you are using to go to the credentials page. If you do not currently have access to the integration you need, contact your Adobe Account Team.

To finish creating the connection, you need the following info:

*  The public address of your RDS instance: This can be found in the [!DNL AWS] management console.
*  The port your database instance uses: Some databases have a default port, which automatically populates the `Port` field. This info can also be found in the setup documentation for the database.
*  The username and password of the user you created for [!DNL Commerce Intelligence].

If you are using an encrypted connection, change the `Encrypted` toggle on the database credentials page to `Yes`. This displays an extra form for setting up the encryption:

![SQL integration form with encryption enabled showing Yes option](../../../assets/sql-integration-encrypted-yes.png)



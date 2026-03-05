---
title: Connect databases via VPN
description: Learn how to connect databases via VPN instead of SSH Tunnel.
exl-id: c7aa564d-42de-426e-92e9-f6e250a6abba
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/0B7swwGIgBemitnx8Q4tyN8VtqwzcA-DYZdXHqzyNAk
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
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
---
# Connect databases via VPN

While Adobe recommends that you connect your databases using an `SSH tunnel`, you can also use an encrypted `VPN` connection to keep things secure. A `VPN` can be used for any of your database integrations and, to keep things simple, the process is just about the same as setting up an `SSH tunnel`:

1. [Create an [!DNL Commerce Intelligence] database user](#database)
1. [Create an [!DNL Commerce Intelligence] VPN user](#vpn)
1. [Allow access to the [!DNL Commerce Intelligence] IP address](#allowlist)
1. [Enter the connection and VPN user info into Commerce Intelligence](#finish)

In addition to database credentials, you must enter credentials for a VPN user to wrap things up. Any VPN user works, but Adobe recommends you create an [!DNL Commerce Intelligence] user, as it makes it easier for you to track the users on your account.

## Creating a database user for [!DNL Commerce Intelligence] {#database}

The process for creating a database user varies depending on the database type you are connecting. To see the instructions for each database type, click the links below.

* [Microsoft SQL](../integrations/microsoft-sql-server.md)
* [MongoDB](../integrations/databases-via-a-vpn.md)
* [MySQL](../integrations/mysql-via-a-direct-connection.md)
* [PostgreSQL](../integrations/postgresql.md)

## Creating a `VPN` user for [!DNL Commerce Intelligence] {#vpn}

As mentioned before, any valid `VPN` user works - but Adobe recommends you create a user solely for [!DNL Commerce Intelligence] use.

## Allow access to the [!DNL Commerce Intelligence] IP addresses {#allowlist}

For the connection to be successful, you must configure your firewall to allow access from your IP addresses. They are `54.88.76.97` and `34.250.211.151`, but it is also on the `credentials` page for any database integration:

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## Entering the connection and `VPN` user info into [!DNL Commerce Intelligence] {#finish}

To wrap things up, you need to enter the connection and user info into [!DNL Commerce Intelligence]. Did you leave the database `credentials` page open? If not, go to **[!UICONTROL Manage Data** > **Connections]**. Click **[!UICONTROL Add New Data Source]**, and then click the icon for the database you are connecting. Do not forget to change the `Encrypted` toggle to `Yes`.

Enter the following info into this page, starting with the `Database Connection` section:

* `Username`: The username for the [!DNL Commerce Intelligence] database user
* `Password`: The password for the [!DNL Commerce Intelligence] database user
* `Port`: The database's port on your server. Defaults are:
   * `MicrosoftSQL`: `1433`
   * `MongoDB`: `27017`
   * `MySQL`: `3306`
   * `PostgreSQL`: `5432`
* `Host`: By default, this is localhost `127.0.0.1`, but it could also be your server's public IP address or a local area network address.
* `Database Name (optional)`: If you only allowed access to one database (this is specified during the database user creation step), enter the name of that database here.

Under the `Encryption Connection` section:

* `Encryption Type`: Set this to `Cisco IPsec VPN`
* `Gateway Address`: The IP address of the VPN server
* `Group Name`: The name of the group used for group authentication
* `Group Secret`: The password corresponding to the group.
* `Username`: The [!DNL Commerce Intelligence] `VPN` username
* `Password`: The [!DNL Commerce Intelligence] `VPN` user password

When you are finished, click **[!UICONTROL Save & Test]** to complete the setup.

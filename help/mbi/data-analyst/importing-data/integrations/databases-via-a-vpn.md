---
title: Connect databases via VPN
description: Learn how to connect databases via VPN instead of SSH Tunnel.
exl-id: c7aa564d-42de-426e-92e9-f6e250a6abba
---
# Connect databases via VPN

While [!DNL Adobe] recommends that you connect your databases using an SSH tunnel, you can also use an encrypted VPN connection to keep things secure. A `VPN` can be used for any of your database integrations and, to keep things simple, the process is just about the same as setting up an `SSH tunnel`:

1. [Create an [!DNL Commerce Intelligence] database user](#database)
1. [Create an [!DNL Commerce Intelligence] VPN user](#vpn)
1. [Allow access to the [!DNL Commerce Intelligence] IP address](#allowlist)
1. [Enter the connection and VPN user info into Commerce Intelligence](#finish)

In addition to database credentials, you must enter credentials for a VPN user to wrap things up. Any VPN user works, but [!DNL Adobe] recommends you create an [!DNL Commerce Intelligence] user, as it makes it easier for you to track the users on your account.

## Creating a database user for [!DNL Commerce Intelligence] {#database}

The process for creating a database user varies depending on the database type you are connecting. To see the instructions for each database type, click the links below.

* [Microsoft SQL](../integrations/microsoft-sql-server.md)
* [MongoDB](../integrations/databases-via-a-vpn.md)
* [MySQL](../integrations/mysql-via-a-direct-connection.md)
* [PostgreSQL](../integrations/postgresql.md)

## Creating a `VPN` user for [!DNL Commerce Intelligence] {#vpn}

As mentioned before, any valid `VPN` user works - but [!DNL Adobe] recommends you create a user solely for [!DNL Commerce Intelligence] use.

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

That is it! When you are finished, click **[!UICONTROL Save & Test]** to complete the setup.

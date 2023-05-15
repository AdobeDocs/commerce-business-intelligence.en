---
title: Connect MySQL via cPanel
description: Learn how to connect MySQL via cPanel.
exl-id: 90b0a0b0-8c6b-4144-95b4-f588f18616c7
---
# Connect MySQL via cPanel

* [Create a [!DNL Commerce Intelligence] MySQL user in cPanel](#cpanel)
* [Enter connection and user info into Commerce Intelligence](#finish)

## Jump to

* [MySQL via SSH tunnel](../integrations/mysql-via-ssh-tunnel.md)
* [MySQL via direct connection](../integrations/mysql-via-a-direct-connection.md)

* **`MySQL via cPanel`**

>[!IMPORTANT]
>
>[!DNL Adobe] recommends you use SSH or some other form of encryption to secure your data! If this is not an option, you can still directly connect [!DNL Commerce Intelligence] to your database using the instructions in this article.

This topic walks you through directly connecting your MySQL database to [!DNL Commerce Intelligence] using `cPanel`. This process can also be used to connect [!DNL Adobe Commerce] and any other MySQL-based eCommerce databases to [!DNL Commerce Intelligence].

1. Create an [!DNL Commerce Intelligence] MySQL user in `cPanel`
1. Enter connection and user info into [!DNL Commerce Intelligence]

Get started.

## Creating an [!DNL Commerce Intelligence] MySQL user in `cPanel` {#cpanel}

1. Log in to [`cPanel`](../../../data-analyst/importing-data/integrations/mysql-via-cpanel.md) via your hosting provider.
1. Click **[!UICONTROL MySQL Databases]**, located in the `Database` section.
1. Scroll down to the `Add New User` section and create a user for [!DNL Commerce Intelligence]:

     ![](../../../assets/create-mbi-mysql-user-cpanel.png)

1. Click **[!UICONTROL Create User]**.
1. Now that you have created the user, you need to associate it to a database. Go back to the `Add New User` section - see the settings for `Add User to Database?` That is what you need.
1. In the `User` dropdown of this section, select the user you created.
1. In the `Database` dropdown of this section, select the database you want to connect to [!DNL Commerce Intelligence].
1. Click **[!UICONTROL Add]**.
1. When the checklist of privileges appears, check the box next to `SELECT` - this is all [!DNL Commerce Intelligence] needs to connect to your database.

## Entering the connection and user info into [!DNL Commerce Intelligence] {#finish}

To wrap things up, you need to enter the connection and user info into [!DNL Commerce Intelligence]. Did you leave the MySQL credentials page open? If not, go to **[!UICONTROL Manage Data** > **Connections]** and click **[!UICONTROL Add New Data Source]**, then the MySQL icon.

Enter the following info into this page in the `Database Connection` section:

* `Username`: The username for the [!DNL Commerce Intelligence] MySQL user
* `Password`: The password for the [!DNL Commerce Intelligence] MySQL user
* `Port`: MySQL's port on your server (`3306` by default)
* `Host`: The public address of the `MySQL` server [!DNL Commerce Intelligence] connects to. This is usually the URL that you use to log into `cPanel`.

If you are using an [`SSH tunnel`](../integrations/mysql-via-ssh-tunnel.md), you must enter the encryption information. Set the `Encrypted` toggle to `Yes` to display the form.

* `Connection Type`: Set this to `SSH Tunnel`
* `Remote Address`: The IP address or hostname of the server [!DNL Commerce Intelligence] will tunnel into
* `Username`: The username for the [!DNL Commerce Intelligence] `SSH (Linux)` user, see [instructions](../../../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md) on how to do this, if you have not already)
* `SSH Port`: SSH port on your server (`22` by default)

That is it! When you are finished, click **[!UICONTROL Save & Test]** to complete the setup.

## Related:

* [Reauthenticating integrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)

---
title: Connecting [!DNL MySQL] via SSH tunnel
description: Learn how to connect [!DNL MySQL] via SSH Tunnel.
exl-id: 6b691a6a-9542-4e47-9b1d-d6d3c3dac357
---
# Connect [!DNL MySQL] via [!DNL SSH Tunnel]

* [Retrieve the [!DNL Commerce Intelligence] public key](#retrieve)
* [Allow access to the [!DNL Commerce Intelligence] IP address](#allowlist)
* [Create a Linux user for [!DNL Commerce Intelligence]](#linux)
* [Create a [!DNL MySQL] user for [!DNL Commerce Intelligence]](#mysql)
* [Enter the connection and user info into [!DNL Commerce Intelligence]](#finish)

## JUMP TO

* [!DNL MySQL] via [!DNL SSH Tunnel]
* [[!DNL MySQL] via `direct connection`](../integrations/mysql-via-a-direct-connection.md)
* [[!DNL MySQL] via [!DNL cPanel]](../integrations/mysql-via-cpanel.md)

To connect your [!DNL MySQL] database to [!DNL Commerce Intelligence] via an `SSH tunnel`, you must do a few things:

1. Retrieve the [!DNL Commerce Intelligence] `public key`
1. Allow access to the [!DNL Commerce Intelligence] `IP address`
1. Create a `Linux` user for [!DNL Commerce Intelligence]
1. Create a `MySQL` user for [!DNL Commerce Intelligence]
1. Enter the connection and user info into [!DNL Commerce Intelligence]


## Retrieving the [!DNL Commerce Intelligence] public key {#retrieve}

The `public key` is used to authorize the [!DNL Commerce Intelligence] `Linux` user. In the next section, you will create the user and import the key.

1. Go to **[!UICONTROL Manage Data** > **Connections]** and click **[!UICONTROL Add New Data Source]**.
1. Click the `MySQL` icon.
1. After the `MySQL credentials` page opens, set the `Encrypted` toggle to `Yes`. This displays the SSH setup form.
1. The `public key` is located underneath this form.

Leave this page open throughout the tutorial - you will need it in the next section and at the end.

Here's how to navigate through [!DNL Commerce Intelligence] to retrieve the key:

![](../../../assets/MySQL_SSH.gif)<!--{: width="770"}-->

## Allow access to the [!DNL Commerce Intelligence] IP address {#allowlist}

For the connection to be successful, you must configure your firewall to allow access from your IP addresses. They are `54.88.76.97` and `34.250.211.151` but they are also on the `MySQL credentials` page. See the blue box in the GIF above.

## Creating a [!DNL Linux] user for [!DNL Commerce Intelligence] {#linux}

This can be a production or secondary machine, as long as it contains real-time (or frequently updated) data. You may [restrict this user](../../../administrator/account-management/restrict-db-access.md) any way you like, as long as it retains the right to connect to the `MySQL` server.

1. To add the new user, run the following commands as root on your [!DNL Linux] server:

```bash
        adduser rjmetric -p<password>
        mkdir /home/rjmetric
        mkdir /home/rjmetric/.ssh
```

1. Remember the `public key` you retrieved in the first section? To ensure that the user has access to the database, you need to import the key into `authorized\_keys`.

     Copy the entire key into the `authorized\_keys` file as follows:

```bash
        touch /home/rjmetric/.ssh/authorized_keys
        "<PASTE KEY HERE>" >> /home/rjmetric/.ssh/authorized_keys
```

1. To finish creating the user, alter the permissions on the `/home/rjmetric` directory to allow access via `SSH`:

```bash
        chown -R rjmetric:rjmetric /home/rjmetric
        chmod -R 700 /home/rjmetric/.ssh
        chmod 400 /home/rjmetric/.ssh/authorized_keys
```

>[!IMPORTANT]
>
>If the `sshd\_config` file associated with the server is not set to the default option, only certain users have server access - this prevents a successful connection to [!DNL Commerce Intelligence]. In these cases, it is necessary to run a command like `AllowUsers` to allow the `rjmetric` user access to the server.

## Creating a [!DNL MySQL] user for [!DNL Commerce Intelligence] {#mysql}

Your organization may require a different process, but the simplest way to create this user is to execute the following query when logged into [!DNL MySQL] as a user with the right to grant privileges:

```sql
    GRANT SELECT ON *.* TO 'rjmetric'@'localhost' IDENTIFIED BY '<secure password here>';
```

Replace `secure password here` with a secure password, which can be different from the `SSH` password.

To restrict this user from accessing data in specific databases, tables, or columns, you can instead run GRANT queries that only allow access to the data you permit.

## Entering the connection and user info into [!DNL Commerce Intelligence] {#finish}

To wrap things up, you need to enter the connection and user info into [!DNL Commerce Intelligence]. Did you leave the `MySQL credentials` page open? If not, go to **[!UICONTROL Data** > **Connections]** and click **[!UICONTROL Add New Data Source]**, then the [!DNL MySQL] icon. Do not forget to set the `Encrypted` toggle to `Yes`.

Enter the following info into this page, starting with the `Database Connection` section:

* `Username`: The username for the [!DNL Commerce Intelligence] [!DNL MySQL] user
* `Password`: The password for the [!DNL Commerce Intelligence] [!DNL MySQL] user
* `Port`: [!DNL MySQL] port on your server (3306 by default)
* `Host` By default, this is localhost. In general, it is the bind-address value for your [!DNL MySQL] server, which by default is `127.0.0.1 (localhost)`, but could also be some local network address (for example, `192.168.0.1`) or your server's public IP address.

   The value can be found in your `my.cnf` file (located at `/etc/my.cnf`) underneath the line that reads `\[mysqld\]`. If the bind-address line is commented out in that file, your server is secured from outside connection attempts.

In the `SSH Connection` section:

* `Remote Address`: The IP address or hostname of the server [!DNL Commerce Intelligence] will tunnel into
* `Username`: The username for the [!DNL Commerce Intelligence] SSH ([!DNL Linux]) user
* `SSH Port`: SSH port on your server (22 by default)

When you are finished, click **[!UICONTROL Save & Test]** to complete the setup.

## Related:

* [Reauthenticating integrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)

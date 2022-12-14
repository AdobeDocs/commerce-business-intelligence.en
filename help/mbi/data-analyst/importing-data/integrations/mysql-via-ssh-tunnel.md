---
title: Connecting MySQL via SSH tunnel
description: Learn how to connect MySQL via SSH Tunnel.
exl-id: 6b691a6a-9542-4e47-9b1d-d6d3c3dac357
---
# Connect `MySQL` via `SSH Tunnel`

* [Retrieve the [!DNL MBI] public key](#retrieve)
* [Allow access to the [!DNL MBI] IP address](#allowlist)
* [Create a Linux user for [!DNL MBI]](#linux)
* [Create a MySQL user for [!DNL MBI]](#mysql)
* [Enter the connection and user info into [!DNL MBI]](#finish)

## JUMP TO

* `MySQL via SSH tunnel`
* [`MySQL` via `direct connection`](../integrations/mysql-via-a-direct-connection.md)
* [`MySQL` via `cPanel`](../integrations/mysql-via-cpanel.md)

To connect your `MySQL` database to [!DNL MBI] via an `SSH tunnel`, you (or your team, if you are not a techie) will need to do a few things:

1. Retrieve the [!DNL MBI] `public key`
1. Allow access to the [!DNL MBI] `IP address`
1. Create a `Linux` user for [!DNL MBI]
1. Create a `MySQL` user for [!DNL MBI]
1. Enter the connection and user info into [!DNL MBI]

It is not as complicated as it might sound. Let us get started.

## Retrieving the [!DNL MBI] public key {#retrieve}

The `public key` is used to authorize the [!DNL MBI] `Linux` user. In the next section, we will create the user and import the key.

1. Go to **[!UICONTROL Manage Data** > **Connections]** and click **[!UICONTROL Add New Data Source]**.
1. Click the `MySQL` icon.
1. After the `MySQL credentials` page opens, set the `Encrypted` toggle to `Yes`. This will display the SSH setup form.
1. The `public key` is located underneath this form.

Leave this page open throughout the tutorial - you will need it in the next section and at the end.

If you are a bit lost, here's how to navigate through [!DNL MBI] to retrieve the key:

![](../../../assets/MySQL_SSH.gif)<!--{: width="770"}-->

## Allow access to the [!DNL MBI] IP address {#allowlist}

For the connection to be successful, your must configure your firewall to allow access from our IP addresses. They are `54.88.76.97` and `34.250.211.151` but they're also on the `MySQL credentials` page. See the blue box in the GIF above? That is it!

## Creating a `Linux` user for [!DNL MBI] {#linux}

This can be a production or secondary machine, as long as it contains real-time (or frequently updated) data. You may [restrict this user](../../../administrator/account-management/restrict-db-access.md) any way you like, as long as it retains the right to connect to the `MySQL` server.

1. To add the new user, run the following commands as root on your `Linux` server:

```bash
        adduser rjmetric -p<password>
        mkdir /home/rjmetric
        mkdir /home/rjmetric/.ssh
```

1. Remember the `public key` we retrieved in the first section? To ensure the user has access to the database, we need to import the key into `authorized\_keys`.

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
>If the `sshd\_config` file associated with the server is not set to the default option, only certain users will have server access - this will prevent a successful connection to [!DNL MBI]. In these cases, it is necessary to run a command like `AllowUsers` to allow the `rjmetric` user access to the server.

## Creating a `MySQL` user for [!DNL MBI] {#mysql}

Your organization may require a different process, but the simplest way to create this user is to execute the following query when logged into `MySQL` as a user with the right to grant privileges:

```sql
    GRANT SELECT ON *.* TO 'rjmetric'@'localhost' IDENTIFIED BY '<secure password here>';
```

Replace `secure password here` with a secure password, which can be different than the `SSH` password.

To restrict this user from accessing data in specific databases, tables, or columns, you can instead run GRANT queries that only allow access to the data you permit.

## Entering the connection and user info into [!DNL MBI] {#finish}

To wrap things up, we need to enter the connection and user info into [!DNL MBI]. Did you leave the `MySQL credentials` page open? If not, go to **[!UICONTROL Data** > **Connections]** and click **[!UICONTROL Add New Data Source]**, then the MySQL icon. do not forget to set the `Encrypted` toggle to `Yes`.

Enter the following info into this page, starting with the Database Connection section:

* `Username`: The username for the [!DNL MBI] MySQL user
* `Password`: The password for the [!DNL MBI] MySQL user
* `Port`: MySQL's port on your server (3306 by default)
* `Host` By default, this will be localhost. In general, it will be the bind-address value for your MySQL server, which by default is `127.0.0.1 (localhost)`, but could also be some local network address (for example, `192.168.0.1`) or your server's public IP address.

   The value can be found in your `my.cnf` file (usually located at `/etc/my.cnf`) underneath the line that reads `\[mysqld\]`. If the bind-address line is commented out in that file, your server is secured from outside connection attempts.

In the `SSH Connection` section:

* `Remote Address`: The IP address or hostname of the server [!DNL MBI] will tunnel into
* `Username`: The username for the [!DNL MBI] SSH (Linux) user
* `SSH Port`: SSH port on your server (22 by default)

That is it! When you are finished, click **[!UICONTROL Save & Test]** to complete the setup.

## Related:

* [Reauthenticating integrations](https://support.magento.com/hc/en-us/articles/360016733151)

---
title: Connect PostgreSQL via SSH Tunnel
description: Learn how to connect your PostgreSQL database to Commerce Intelligence via an SSH tunnel.
exl-id: da610988-21c1-4f5f-b4e2-e2deb175a2aa
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export, SQL Report Builder
---
# Connect [!DNL PostgreSQL] via [!DNL SSH Tunnel]

To connect your [!DNL PostgreSQL] database to [!DNL Commerce Intelligence] via an `SSH tunnel`, you must do a few things:

1. [Retrieve the [!DNL Commerce Intelligence] public key](#retrieve)
1. [Allow access to the [!DNL Commerce Intelligence] IP address](#allowlist)
1. [Create a [!DNL Linux] user for [!DNL Commerce Intelligence] ](#linux)
1. [Create a [!DNL PostgreSQL] user for [!DNL Commerce Intelligence] ](#postgres)
1. [Enter the connection and user info into [!DNL Commerce Intelligence]](#finish)

## Retrieving the [!DNL Commerce Intelligence] [!DNL public key] {#retrieve}

The `public key` is used to authorize the [!DNL Commerce Intelligence] [!DNL Linux] user. Now, you will create the user and import the key.

1. Go to **[!UICONTROL Manage Data** > **Connections]** and click **[!UICONTROL Add a Data Source]**.
1. Click the [!DNL PostgreSQL] icon.
1. After the `PostgreSQL credentials` page opens, set the `Encrypted` toggle to `Yes`. This displays the `SSH` setup form.
1. The `public key` is located underneath this form.

Leave this page open throughout the tutorial - you will need it in the next section and at the end.

Below demonstrates how to navigate through [!DNL Commerce Intelligence] to retrieve the key:

![Retrieving the RJMetrics public key](../../../assets/get-mbi-public-key.gif) 

## Allow access to the [!DNL Commerce Intelligence] IP address {#allowlist}

For the connection to be successful, you must configure your firewall to allow access from your IP address. It is `54.88.76.97/32`, but it is also on the `PostgreSQL` credentials page. See the blue box in the GIF above.

## Creating a [!DNL Linux] user for [!DNL Commerce Intelligence] {#linux}

This can be a production or secondary machine, as long as it contains real-time (or frequently updated) data. You may [restrict this user](../../../administrator/account-management/restrict-db-access.md) any way you like, as long as it retains the right to connect to the [!DNL PostgreSQL] server.

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
```

>[!IMPORTANT]
>
>If the `sshd\_config` file associated with the server is not set to the default option, only certain users have server access - this prevents a successful connection to [!DNL Commerce Intelligence]. In these cases, it is necessary to run a command like `AllowUsers` to allow the rjmetric user access to the server.

## Creating an [!DNL Commerce Intelligence] [!DNL Postgres] user {#postgres}

Your organization may require a different process, but the simplest way to create this user is to execute the following query when logged into Postgres as a user with the right to grant privileges. The user should also own the schema that [!DNL Commerce Intelligence] is being granted access to.

```sql
    GRANT CONNECT ON DATABASE <database name> TO rjmetric WITH PASSWORD <secure password>;GRANT USAGE ON SCHEMA <schema name> TO rjmetric;GRANT SELECT ON ALL TABLES IN SCHEMA <schema name> TO rjmetric;ALTER DEFAULT PRIVILEGES IN SCHEMA <schema name> GRANT SELECT ON TABLES TO rjmetric;
```

Replace `secure password` with your own secure password, which can be different from the SSH password. Also, make sure you replace `database name` and `schema name` with the appropriate names in your database.

If you want to connect multiple databases or schemas, repeat this process as necessary.

## Entering the connection and user info into [!DNL Commerce Intelligence] {#finish}

To wrap things up, you need to enter the connection and user info into [!DNL Commerce Intelligence]. Did you leave the [!DNL PostgreSQL] credentials page open? If not, go to **[!UICONTROL Manage Data > Connections]** and click **[!UICONTROL Add a Data Source]**, then the [!DNL PostgreSQL] icon. Do not forget to set the `Encrypted` toggle to `Yes`.

Enter the following info into this page, starting with the `Database Connection` section:

* `Username`: The RJMetrics Postgres username (should be rjmetric)
* `Password`: The RJMetrics Postgres password
* `Port`: PostgreSQL port on your server (5432 by default)
* `Host`: 127.0.0.1

Under `SSH Connection`:

* `Remote Address`: The IP address or hostname of the server you will SSH into
* `Username`: Your SSH login name (should be rjmetric)
* `SSH Port`: SSH port on your server (22 by default)

When you are finished, click **Save & Test** to complete the setup.

### Related

* [Reauthenticating integrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)

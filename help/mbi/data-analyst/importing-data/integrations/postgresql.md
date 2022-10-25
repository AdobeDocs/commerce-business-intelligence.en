---
title: Connect PostgreSQL via SSH Tunnel
description: Learn how to connect your PostgreSQL database to [!DNL MBI] via an SSH tunnel.
---
# Connect PostgreSQL via SSH Tunnel

To connect your PostgreSQL database to [!DNL MBI] via an SSH tunnel, you (or your team, if you are not a techie) will need to do a few things:

1. [Retrieve the [!DNL MBI] public key](#retrieve)
1. [Allow access to the [!DNL MBI] IP address](#allowlist)
1. [Create a Linux user for [!DNL MBI] ](#linux)
1. [Create a Postgres user for [!DNL MBI] ](#postgres)
1. [Enter the connection and user info into MBI](#finish)

It is not as complicated as it might sound. Get started.

## Retrieving the [!DNL MBI] public key {#retrieve}

The public key is used to authorize the [!DNL MBI] Linux user. In the next section, we will create the user and import the key.

1. Go to **Manage Data > Connections** and click **Add a Data Source**.
1. Click the **PostgreSQL icon**.
1. After the PostgreSQL credentials page opens, set the _Encrypted_ toggle to `Yes`. This will display the SSH setup form.
1. The public key is located underneath this form.

Leave this page open throughout the tutorial - you will need it in the next section and at the end.

If you are a bit lost, this is how to navigate through [!DNL MBI] to retrieve the key:

![Retrieving the RJMetrics public key](../../../assets/get-mbi-public-key.gif) 

## Allow access to the [!DNL MBI] IP address {#allowlist}

For the connection to be successful, your must configure your firewall to allow access from our IP address. it is **54.88.76.97/32**, but it is also on the PostgreSQL credentials page. See the blue box in the GIF above? That is it!

## Creating a Linux user for [!DNL MBI] {#linux}

This can be a production or secondary machine, as long as it contains real-time (or frequently updated) data. You may [restrict this user](../../../administrator/account-management/restrict-db-access.md) any way you like, as long as it retains the right to connect to the PostgreSQL server.

1. To add the new user, run the following commands as root on your Linux server:

```bash
        adduser rjmetric -p<password>
        mkdir /home/rjmetric
        mkdir /home/rjmetric/.ssh
```

1. Remember the public key we retrieved in the first section? To ensure the user has access to the database, we need to import the key into authorized\_keys.

     Copy the entire key into the authorized\_keys file as follows:

```bash
        touch /home/rjmetric/.ssh/authorized_keys
        "<PASTE KEY HERE>" >> /home/rjmetric/.ssh/authorized_keys
```

1. To finish creating the user, alter the permissions on the /home/rjmetric directory to allow access via SSH:

```bash
        chown -R rjmetric:rjmetric /home/rjmetric
        chmod -R 700 /home/rjmetric/.ssh
```

**Important!**

If the **sshd\_config** file associated with the server is not set to the default option, only certain users will have server access - this will prevent a successful connection to [!DNL MBI]. In these cases, it is necessary to run a command like **AllowUsers** to allow the rjmetric user access to the server.

## Creating an [!DNL MBI] Postgres user {#postgres}

Your organization may require a different process, but the simplest way to create this user is to execute the following query when logged into Postgres as a user with the right to grant privileges. The user should also own the schema that [!DNL MBI] is being granted access to.

```sql
    GRANT CONNECT ON DATABASE <database name> TO rjmetric WITH PASSWORD <secure password>;GRANT USAGE ON SCHEMA <schema name> TO rjmetric;GRANT SELECT ON ALL TABLES IN SCHEMA <schema name> TO rjmetric;ALTER DEFAULT PRIVILEGES IN SCHEMA <schema name> GRANT SELECT ON TABLES TO rjmetric;
```

Replace `secure password` with a secure password, which can be different than the SSH password. Additionally, make sure you replace `database name` and `schema name` with the appropriate names in your database.

If you want to connect multiple databases or schemas, repeat this process as necessary.

## Entering the connection and user info into [!DNL MBI] {#finish}

To wrap things up, we need to enter the connection and user info into [!DNL MBI].L MBI]. Did you leave the PostgreSQL credentials page open? If not, go to **Manage Data > Connections** and click **Add a Data Source**, then the PostgreSQL icon. do not forget to set the _Encrypted_ toggle to `Yes`.

Enter the following info into this page, starting with the Database Connection section:

* **Username:** The RJMetrics Postgres username (should be rjmetric)
* **Password:** The RJMetrics Postgres password
* **Port:** PostgreSQL port on your server (5432 by default)
* **Host:** 127.0.0.1

Under "SSH Connection":

* **Remote Address:** The IP address or hostname of the server we will SSH into
* **Username:** Our SSH login name (should be rjmetric)
* **SSH Port:** SSH port on your server (22 by default)
That is it! When you are finished, click **Save & Test** to complete the setup.

### Related

* [Reauthenticating integrations](https://support.magento.com/hc/en-us/articles/360016733151)


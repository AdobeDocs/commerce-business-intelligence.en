---
title: Connecting MySQL via SSH tunnel
zendesk_id: 360016506672
---

* [Retrieve the Magento BI public key](#retrieve)
* [Allow access to the Magento BI IP address](#allowlist)
* [Create a Linux user for Magento BI](#linux)
* [Create a MySQL user for Magento BI](#mysql)
* [Enter the connection and user info into Magento BI](#finish)

## JUMP TO

* **MySQL via SSH tunnel**
* [MySQL via direct connection]({% link data-analyst/importing-data/integrations/mysql-via-a-direct-connection.md %})
* [MySQL via cPanel]({% link data-analyst/importing-data/integrations/mysql-via-cpanel.md %})

To connect your MySQL database to Magento BI via an SSH tunnel, you (or your team, if you\'re not a techie) will need to do a few things:

1. Retrieve the Magento BI public key
1. Allow access to the Magento BI IP address
1. Create a Linux user for Magento BI
1. Create a MySQL user for Magento BI
1. Enter the connection and user info into Magento BI

It\'s not as complicated as it might sound. Let\'s get started.

## Retrieving the Magento BI public key {#retrieve}

The public key is used to authorize the Magento BI Linux user. In the next section, we\'ll create the user and import the key.

1. Go to **Manage** **Data &gt; Connections** and click the Add New Data Source button.
1. Click the MySQL icon.
1. After the MySQL credentials page opens, toggle the Encrypted button to Yes. This will display the SSH setup form.
1. The public key is located underneath this form.

Leave this page open throughout the tutorial - you\'ll need it in the next section and at the end.

If you\'re a bit lost, here\'s how to navigate through Magento BI to retrieve the key:

![]({% link images/MySQL_SSH.gif %}){: width="778"}

## Allow access to the Magento BI IP address {#allowlist}

For the connection to be successful, your must configure your firewall to allow access from our IP addresses. They are **54.88.76.97** and **34.250.211.151** but they\'re also on the MySQL credentials page. See the blue box in the GIF above? That\'s it!

## Creating a Linux user for Magento BI {#linux}

This can be a production or secondary machine, as long as it contains real-time (or frequently updated) data. You may [restrict this user]({% link administrator/account-management/restrict-db-access.md %}) any way you like, as long as it retains the right to connect to the MySQL server.

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
        chmod 400 /home/rjmetric/.ssh/authorized_keys
```

**Important!**

If the **sshd\_config** file associated with the server is not set to the default option, only certain users will have server access - this will prevent a successful connection to Magento BI. In these cases, it\'s necessary to run a command like **AllowUsers** to allow the rjmetric user access to the server.

## Creating a MySQL user for Magento BI {#mysql}

Your organization may require a different process, but the simplest way to create this user is to execute the following query when logged into MySQL as a user with the right to grant privileges:

```sql
    GRANT SELECT ON *.* TO 'rjmetric'@'localhost' IDENTIFIED BY '<secure password here>';
```

Replace *&lt;secure password here&gt;* with a secure password, which can be different than the SSH password.

To restrict this user from accessing data in specific databases, tables, or columns, you can instead run GRANT queries that only allow access to the data you permit.

## Entering the connection and user info into Magento BI {#finish}

To wrap things up, we need to enter the connection and user info into Magento BI. Did you leave the MySQL credentials page open? If not, go to **Data > Connections** and click the Add New Data Source button, then the MySQL icon. Don\'t forget to toggle the Encrypted button to Yes.

Enter the following info into this page, starting with the Database Connection section:

* **Username:** The username for the Magento BI MySQL user
* **Password:** The password for the Magento BI MySQL user
* **Port:** MySQL\'s port on your server (3306 by default)
* **Host:** By default, this will be localhost. In general, it will be the bind-address value for your MySQL server, which by default is 127.0.0.1 (localhost), but could also be some local network address (e.g. 192.168.0.1) or your server\'s public IP address.

   The value can be found in your my.cnf file (usually located at \"/etc/my.cnf\") underneath the line that reads \"\[mysqld\]\". If the bind-address line is commented out in that file, your server is secured from outside connection attempts.

In the SSH Connection section:

* **Remote Address:** The IP address or hostname of the server Magento BI will tunnel into
* **Username:** The username for the Magento BI SSH (Linux) user
* **SSH Port:** SSH port on your server (22 by default)

That\'s it! When you\'re finished, click the Save & Test button to complete the setup.

## Related:

* [Reauthenticating integrations](https://support.magento.com/hc/en-us/articles/360016733151)

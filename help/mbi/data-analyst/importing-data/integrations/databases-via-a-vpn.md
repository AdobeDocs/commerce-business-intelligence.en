---
title: Connecting databases via a VPN
zendesk_id: 360016504992
---

While we recommend you connect your databases using an SSH tunnel, you can also use an encrypted VPN connection to keep things secure. A VPN can be used for any of our database integrations and, to keep things simple, the process is just about the same as setting up an SSH tunnel:

1. [Create an Magento BI database user](#database)
1. [Create an Magento BI VPN user](#vpn)
1. [Allow access to the Magento BI IP address](#allowlist)
1. [Enter the connection and VPN user info into Magento BI](#finish)

In addition to database credentials, you\'ll have to enter credentials for a VPN user to wrap things up. Any VPN user will work, but we recommend you create an Magento BI user - it\'ll make it easier for you to keep track of the users on your account.

Let's get started.

## Creating a database user for Magento BI {#database}

The process for creating a database user will vary depending on the database type you\'re connecting. To see the instructions for each database type, click the links below.

* [Microsoft SQL]({% link data-analyst/importing-data/integrations/microsoft-sql-server.md %})
* [MongoDB]({% link data-analyst/importing-data/integrations/databases-via-a-vpn.md %})
* [MySQL]({% link data-analyst/importing-data/integrations/mysql-via-a-direct-connection.md %})
* [PostgreSQL]({% link data-analyst/importing-data/integrations/postgresql.md %})

## Creating a VPN user for Magento BI {#vpn}

As we mentioned before, any valid VPN user will work - but we strongly recommend you create a user solely for Magento BI use.

## Allow access to the Magento BI IP addresses {#allowlist}

For the connection to be successful, your must configure your firewall to allow access from our IP addresses. They are 54.88.76.97 and 34.250.211.151, but it's also on the credentials page for any database integration:

![MBI_Allow_Access_IPs.png]({% link images/MBI_allow_access_IPs.png %})

## Entering the connection and VPN user info into Magento BI {#finish}

To wrap things up, we need to enter the connection and user info into Magento BI. Did you leave the database credentials page open? If not, go to **Manage Data > Connections** and click the Add New Data Source button, then the icon for the database you\'re connecting. Don\'t forget to toggle the Encrypted button to Yes.

Enter the following info into this page, starting with the Database Connection section:

* **Username:** The username for the Magento BI database user
* **Password:** The password for the Magento BI database user
* **Port:** The database\'s port on your server. Defaults are:
* **MicrosoftSQL:** 1433
* **MongoDB:** 27017
* **MySQL:** 3306
* **PostgreSQL:** 5432
* **Host:** By default, this will be localhost (127.0.0.1), but it could also be your server\'s public IP address or a local area network address.
* **Database Name (optional):** If you only allowed access to one database (this is specified during the database user creation step), enter the name of that database here.

Under the Encryption Connection section:

* **Encryption Type:** Set this to Cisco IPsec VPN
* **Gateway Address:** The IP address of the VPN server
* **Group Name:** The name of the group used for group authentication
* **Group Secret:** The password corresponding to the group.
* **Username:** The Magento BI VPN username
* **Password:** The Magento BI VPN user password

That\'s it! When you\'re finished, click the Save & Test button to complete the setup.

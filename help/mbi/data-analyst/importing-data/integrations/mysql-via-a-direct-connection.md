---
title: Connecting MySQL via a direct connection
zendesk_id: 360016506312
---

## IN THIS ARTICLE

* [Allow access to the MBI IP address](../#allowlist)
* [Create a MySQL user for MBI](../#steptwo)
* [Enter connection info into MBI](../#stepthree)

## JUMP TO

* [MySQL via SSH tunnel](../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md)
* **MySQL via direct connection**
* [MySQL via cPanel](../data-analyst/importing-data/integrations/mysql-via-cpanel.md)

**One thing we take seriously is data security. We strongly recommend you use [SSH](../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md) or some other form of encryption to secure your data!** If this is not an option, you can still directly connect MBI to your database using the instructions in this article.

In this article, we will walk you through directly connecting your MySQL database to MBI. These settings can also be used with Magento EE/CE or any other eCommerce databases that use MySQL.

## Allow access to the MBI IP addresses {#allowlist}

For the connection to be successful, your must configure your firewall to allow access from our IP addresses. They are **54.88.76.97** and **34.250.211.151**, but it is also on the MySQL credentials page:

![MBI_Allow_Access_IPs.png](../../assets/MBI_allow_access_IPs.png)

## <span id="steptwo">Create a MySQL user for MBI</span>

The simplest way to create a MySQL user for MBI is to execute the following query when logged into MySQL with GRANT privileges. Replace *&lt;MBI IP Address&gt;* with the MBI IP address and replace *&lt;secure password&gt;* with a secure password of your choice:

```sql
    GRANT SELECT ON *.* TO 'magentobi'@'<MBI IP address>' IDENTIFIED BY '<secure password>';
```

To restrict this user from accessing data in specific databases, tables, or columns, you can instead run GRANT queries that only allow access to the data you permit.

**Please re-run the GRANT query for all required IPs using the same user and password.**

## <span id="stepthree">Enter connection info in MBI</span>

To wrap things up, we need to enter the connection and user info into MBI. Did you leave the MySQL credentials page open? If not, go to **Data &gt; Connections** and click the Add New Data Source button, then the MySQL icon. do not forget to toggle the Encrypted button to Yes.

Enter the following info into this page, starting with the Database Connection section:

* **Connection Nickname:** Enter a name for the integration (ex: Ecommerce Store)
* **Username:** The username for the MBI MySQL user
* **Password:** The password for the MBI MySQL user
* **Port:** MySQL's port on your server (3306 by default)
* **Host:** By default, this will be localhost. In general, it will be the bind-address value for your MySQL server, which by default is 127.0.0.1 (localhost), but could also be some local network address (e.g., 192.168.0.1) or your server's public IP address.

   The value can be found in your my.cnf file (usually located at "/etc/my.cnf") underneath the line that reads "\[mysqld\]". If the bind-address line is commented out in that file, your server is secured from outside connection attempts.

That's it! When you are finished, click the Save & Test button to complete the setup.

## Related documentation

* [Reauthenticating integrations](https://support.magento.com/hc/en-us/articles/360016733151)

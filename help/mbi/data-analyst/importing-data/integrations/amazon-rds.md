---
title: Connecting Amazon RDS
zendesk_id: 360016730931
---

Amazon Relational Database Services (RDS) is a managed database service that runs on database engines that you are probably already familiar with - [MySQL](../integrations/mysql-via-a-direct-connection.md), [Microsoft SQL](../integrations/microsoft-sql-server.md), and [PostgreSQL](../integrations/postgresql.md).

The steps for connecting your RDS instance vary slightly depending on the type of database you are using (use the links above for detailed instructions for each database), and whether or not you are using an encrypted connection ([like an SSH tunnel for MySQL](../integrations/mysql-via-ssh-tunnel.md)), but here's the gist of it:

## Authorize MBI to access your database

On the credentials page (**Manage Data &gt; Integrations**) for each database, you will see a box containing the IP addresses you will need to authorize to connect RDS to MBI: **54.88.76.97** and **34.250.211.151**. Here's a look at the MySQL credentials page, where we highlighted the IP address box:

![](../../../assets/RDS_IP.png)

For MBI to successfully connect with your RDS instance, you will need to add these IP addresses to the appropriate database security group via the AWS management console. These IP addresses can be added to an existing group or you can create a new one - the important thing is that the group is authorized to access the instance you want to connect to MBI.

When adding the MBI IP addresses, make sure you add a "/32" to the end of the address to indicate to Amazon that it is an exact IP address. do not worry; the AWS interface will make it clear that this is required.

## Create a Linux user for MBI {#linux}

**This step is only required if you are using an encrypted connection.** For instructions on how to do this, refer to the setup article for the database you are using (ex: MySQL). The Linux user will allow us to create an SSH tunnel, which is the safest method of sending data over the internet.

## Create a database user for MBI

This is the part of the process where, depending on the database you are using, the steps will vary. The idea is the same, though: you will create a user for MBI which will be used to access your database. Instructions for creating a database MBI user can be found in the setup article for the database you are using.

## Enter connection info into MBI

After you have granted MBI access to your instance and created a user for us, the last thing you will need to do is enter the connection info into MBI.

The credential pages for MySQL, Microsoft SQL, and PostgreSQL are accessed via the Integrations page (**Manage Data &gt; Integrations**) by clicking the **Add Integration** button. When the list of integrations displays, click the icon for the database you are using to go to the credentials page. If you do not currently have access to the integration you need, contact your CSM.

To finish creating the connection, we will need the following info:

*  **The public address of your RDS instance**. This can be found in the AWS management console.
*  **The port your database instance uses**. Some databases have a default port, which will automatically populate the Port field. This info can also be found in our setup documentation for the database.
*  The username and password of the user you created for MBI

Additionally, **if you are using an encrypted connection**, toggle the Encrypted button on the database credentials page to Yes. This will display an additional form for setting up the encryption:

![](../../../assets/5.1.png)

That's all there is to it! Connecting your RDS instance is complete.

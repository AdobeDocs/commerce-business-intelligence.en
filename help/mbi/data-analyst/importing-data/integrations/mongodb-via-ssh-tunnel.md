---
title: Connect MongoDB via SSH tunnel
description: Learn how to connect MongoDB via SSH tunnel.
---
# Connect MongoDB via SSH Tunnel 


To connect your MongoDB database to [!DNL MBI] via an SSH tunnel, you (or your team, if you are not a techie) will need to do a few things:

1. [Retrieve the [!DNL MBI] public key](#retrieve)
1. [Allow access to the [!DNL MBI] IP address](#allowlist)
1. [Create a Linux user for MBI](#linux)
1. [Create a MongoDB user for MBI](#mongodb)
1. [Enter the connection and user info into MBI](#finish)

>[!NOTE]
>
>Due to the technical nature of this setup, we suggest you loop in a developer to help out if you have not done this before.

## Retrieving the [!DNL MBI] public key {#retrieve}

The public key is used to authorize the [!DNL MBI] Linux user. In the next section, we create the user and import the key.

1. Go to **Data > Connections** and click **Add New Data Source**.
1. Click the **MongoDB** icon.
1. After the MongoDB credentials page opens, change the **Encrypted** toggle to `Yes`. This will display the SSH setup form.
1. The public key is located underneath this form.

Leave this page open throughout the tutorial - you will need it in the next section and at the end.

If you are a bit lost, Here is how to navigate through [!DNL MBI] to retrieve the key:

![Retrieving the RJMetrics public key](../../../assets/MongoDB_Public_Key.gif)<!--{:.zoom}-->

## Allow access to the [!DNL MBI] IP address {#allowlist}

For the connection to be successful, your must configure your firewall to allow access from our IP addresses. They are **54.88.76.97** and **34.250.211.151**, but it is also on the MongoDB credentials page:

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## Creating a Linux user for [!DNL MBI] {#linux}

**Important!**
 If the `sshd_config` file associated with the server is not set to the default option, only certain users will have server access - this will prevent a successful connection to MBI. In these cases, it is necessary to run a command like `AllowUsers` to allow the rjmetric user access to the server.

This can be a production or secondary machine, as long as it contains real-time (or frequently updated) data. You may restrict this user any way you like as long as it retains the right to connect to the MongoDB server.

To add the new user, run the following commands as root on your Linux server:

```bash
    adduser rjmetric -p
    mkdir /home/rjmetric
    mkdir /home/rjmetric/.ssh
```

Remember the public key we retrieved in the first section? To ensure the user has access to the database, we need to import the key into `authorized_keys`. Copy the entire key into the `authorized_keys` file as follows:

```bash
    touch /home/rjmetric/.ssh/authorized_keys
    "< PASTE KEY HERE >" >> /home/rjmetric/.ssh/authorized_keys
```

To finish creating the user, alter the permissions on the /home/rjmetric directory to allow access via SSH:

```bash
    chown -R rjmetric:rjmetric /home/rjmetric
    chmod -R 700 /home/rjmetric/.ssh
```

## Creating an [!DNL MBI] MongoDB user {#mongodb}

MongoDB servers have two run modes - [one with the "auth" option](#auth) `(mongod -- auth)` and one without, [which is the default](#default). The steps for creating a MongoDB user will vary a bit depending on what mode your server is using, so be sure to verify the mode before continuing.

### If your server uses the Auth Option: {#auth}

When connecting to multiple databases, you can add the user by logging into MongoDB as an admin user and running the following commands. **Note that to see all available databases, the [!DNL MBI] user requires the permissions to run `listDatabases.`**

This command will grant the [!DNL MBI] user access **to all databases**:

```bash
    use admin
    db.createUser('rjmetric', '< secure password here >', true)
```

Use this command to grant the [!DNL MBI] user access **to a single database**:

```bash
    use < database name >
    db.createUser('rjmetric', '< secure password here >', true)
```

This will print a response that looks like this:

```bash
    {
    "id": ObjectId("< some object id here >"),
    "user": "rjmetric",
    "readOnly": true,
    "pwd": "< some hash here >"
    }
```

### If your server uses the default option {#default}

If your server does not use auth mode, your MongoDB server will still be accessible even without a username and password. However, you should ensure the mongodb.conf file `(/etc/mongodb.conf)` has the following lines - if they're not there, restart your server after you add them.

```bash
    bind_ip = 127.0.0.1
    noauth = true
```

To bind your MongoDB server to a different address, adjust the database hostname in the next step accordingly.

## Entering the connection and user info into [!DNL MBI] {#finish}

To wrap things up, we need to enter the connection and user info into MBI. Did you leave the MongoDB credentials page open? If not, go to **Data > Connections** and click **Add New Data Source**, then the MongoDB icon. do not forget to change the _Encrypted_ toggle to `Yes`.

Enter the following info into this page, starting with the Database Connection section:

* **Host:**127.0.0.1
* **Username:** The [!DNL MBI] MongoDB username (should be rjmetric)
* **Password:**The [!DNL MBI] MongoDB password
* **Port:**MongoDB's port on your server (27017 by default)
* **Database Name (Optional):**If you only allowed access to one database, specify the name of that database here.

Under the SSH Connection section:

* **Remote Address:**The IP address or hostname of the server we will SSH into
* **Username:**The [!DNL MBI] Linux (SSH) username (should be rjmetric)
* **SSH Port:**The SSH port on your server (22 by default)

That is it! When you are finished, click **Save Test** to complete the setup.

### Related

* [Reauthenticating integrations](https://support.magento.com/hc/en-us/articles/360016733151)


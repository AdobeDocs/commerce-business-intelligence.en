---
title: Connect [!DNL MongoDB] via SSH tunnel
description: Learn how to connect [!DNL MongoDB] via SSH tunnel.
exl-id: 3557a8c7-c4c5-4742-ae30-125c719aca39
---
# Connect [!DNL MongoDB] via SSH Tunnel 

To connect your [!DNL MongoDB] database to [!DNL Commerce Intelligence] via an SSH tunnel, you (or your team, if you are not a techie) must do a few things:

1. [Retrieve the [!DNL Commerce Intelligence] public key](#retrieve)
1. [Allow access to the [!DNL Commerce Intelligence] IP address](#allowlist)
1. [Create a Linux&reg; user for Commerce Intelligence](#linux)
1. [Create a [!DNL MongoDB] user for Commerce Intelligence](#mongodb)
1. [Enter the connection and user info into [!DNL Commerce Intelligence]](#finish)

>[!NOTE]
>
>Due to the technical nature of this setup, Adobe recommends you loop in a developer to help out if you have not done this before.

## Retrieving the [!DNL Commerce Intelligence] public key {#retrieve}

The `public key` is used to authorize the [!DNL Commerce Intelligence] `Linux` user. The next section walks you through creating the user and import the keys.

1. Go to **[!UICONTROL Data** > **Connections]** and click **[!UICONTROL Add New Data Source]**.
1. Click the [!DNL MONGODB] icon.
1. After the [!DNL MongoDB] credentials page opens, change the `Encrypted` toggle to `Yes`. This displays the SSH setup form.
1. The `public key` is located underneath this form.

Leave this page open throughout the tutorial - you will need it in the next section and at the end.

If you are a bit lost, here is how to navigate through [!DNL Commerce Intelligence] to retrieve the key:

![Retrieving the RJMetrics public key](../../../assets/MongoDB_Public_Key.gif)<!--{:.zoom}-->

## Allow access to the [!DNL Commerce Intelligence] IP address {#allowlist}

For the connection to be successful, you must configure your firewall to allow access from your IP addresses. They are `54.88.76.97` and `34.250.211.151`, but it is also on the [!DNL MongoDB] credentials page:

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## Creating a `Linux` user for [!DNL Commerce Intelligence] {#linux}

>[!IMPORTANT]
>
>If the `sshd_config` file associated with the server is not set to the default option, only certain users have server access - this prevents a successful connection to [!DNL Commerce Intelligence]. In these cases, it is necessary to run a command like `AllowUsers` to allow the `rjmetric` user access to the server.

This can be a production or secondary machine, as long as it contains real-time (or frequently updated) data. You may restrict this user any way you like as long as it retains the right to connect to the [!DNL MongoDB] server.

To add the new user, run the following commands as root on your `Linux` server:

```bash
    adduser rjmetric -p
    mkdir /home/rjmetric
    mkdir /home/rjmetric/.ssh
```

Remember the `public key` you retrieved in the first section? To ensure that the user has access to the database, you need to import the key into `authorized_keys`. Copy the entire key into the `authorized_keys` file as follows:

```bash
    touch /home/rjmetric/.ssh/authorized_keys
    "< PASTE KEY HERE >" >> /home/rjmetric/.ssh/authorized_keys
```

To finish creating the user, alter the permissions on the /home/rjmetric directory to allow access via SSH:

```bash
    chown -R rjmetric:rjmetric /home/rjmetric
    chmod -R 700 /home/rjmetric/.ssh
```

## Creating an [!DNL Commerce Intelligence] [!DNL MongoDB] user {#mongodb}

[!DNL MongoDB] servers have two run modes - [one with the "auth" option](#auth) `(mongod -- auth)` and one without, [which is the default](#default). The steps for creating a [!DNL MongoDB] user varies depending on what mode your server is using. Bee sure to verify the mode before continuing.

### If your server uses the `Auth` Option: {#auth}

When connecting to multiple databases, you can add the user by logging into [!DNL MongoDB] as an admin user and running the following commands.

>[!NOTE]
>
>To see all available databases, the [!DNL Commerce Intelligence] user requires the permissions to run `listDatabases.`

This command grants the [!DNL Commerce Intelligence] user access `to all databases`:

```bash
    use admin
    db.createUser('rjmetric', '< secure password here >', true)
```

Use this command to grant the [!DNL Commerce Intelligence] user access `to a single database`:

```bash
    use < database name >
    db.createUser('rjmetric', '< secure password here >', true)
```

This prints a response that looks like this:

```bash
    {
    "id": ObjectId("< some object id here >"),
    "user": "rjmetric",
    "readOnly": true,
    "pwd": "< some hash here >"
    }
```

### If your server uses the default option {#default}

If your server does not use `auth` mode, your [!DNL MongoDB] server is accessible even without a username and password. However, you should ensure the `mongodb.conf` file `(/etc/mongodb.conf)` has the following lines - if not, restart your server after you add them.

```bash
    bind_ip = 127.0.0.1
    noauth = true
```

To bind your [!DNL MongoDB] server to a different address, adjust the database hostname in the next step accordingly.

## Entering the connection and user info into [!DNL Commerce Intelligence] {#finish}

To wrap things up, you need to enter the connection and user info into [!DNL Commerce Intelligence]. Did you leave the [!DNL MongoDB] credentials page open? If not, go to **[!UICONTROL Data > Connections]** and click **[!UICONTROL Add New Data Source]**, then the [!DNL MongoDB] icon. Do not forget to change the `Encrypted` toggle to `Yes`.

Enter the following info into this page, starting with the `Database Connection` section:

* `Host`: `127.0.0.1`
* `Username`: The [!DNL Commerce Intelligence] [!DNL MongoDB] username (should be `rjmetric`)
* `Password`: The [!DNL Commerce Intelligence] [!DNL MongoDB] password
* `Port`: MongoDB's port on your server (`27017` by default)
* `Database Name` (Optional): If you only allowed access to one database, specify the name of that database here.

Under the `SSH Connection` section:

* `Remote Address`: The IP address or hostname of the server you will SSH into
* `Username`: The [!DNL Commerce Intelligence] Linux&reg; (SSH) username (should be rjmetric)
* `SSH Port`: The SSH port on your server (22 by default)

That is it! When you are finished, click **[!UICONTROL Save Test]** to complete the setup.

### Related

* [Reauthenticating integrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)

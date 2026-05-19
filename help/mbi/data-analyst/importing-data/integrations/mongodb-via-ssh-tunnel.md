---
title: Connect [!DNL MongoDB] via SSH tunnel
description: Learn how to connect [!DNL MongoDB] via SSH tunnel, enroll SSH host keys, refresh trust material, and resolve SSH host key errors.
exl-id: 3557a8c7-c4c5-4742-ae30-125c719aca39
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/fYXQ353R-dPB-rSeYCR2w0c8Lp5I0HoVYh1A3UAI6aI
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
---
# Connect [!DNL MongoDB] via SSH Tunnel 

To connect your [!DNL MongoDB] database to [!DNL Commerce Intelligence] via an SSH tunnel, you must do a few things:

1. [Retrieve the [!DNL Commerce Intelligence] public key](#retrieve)
1. [Allow access to the [!DNL Commerce Intelligence] IP address](#allowlist)
1. [Create a Linux user for Commerce Intelligence](#linux)
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
* `Username`: The [!DNL Commerce Intelligence] Linux (SSH) username (should be rjmetric)
* `SSH Port`: The SSH port on your server (22 by default)

When you are finished, click **[!UICONTROL Save & Test]** to complete the setup.

## SSH host key verification {#ssh-host-keys}

[!DNL Commerce Intelligence] uses strict SSH host key verification for encrypted (SSH tunnel) connections. During **[!UICONTROL Save & Test]**, the system enrolls the SSH bastion host keys for your connection and stores them securely per connection. After enrollment, replication and tunneling only succeed when the live bastion host keys match the enrolled keys.

This model improves security by blocking man-in-the-middle and unexpected host changes. It also means that host key rotation, missing trust material, or infrastructure changes can surface as SSH host key errors on the connection instead of generic tunnel failures.

>[!NOTE]
>
>Only Admin users can run **[!UICONTROL Refresh SSH Host Keys]**. If you do not see this control, ask an Admin on your account to run the refresh or contact Adobe Support.

### Expected behavior for Save & Test {#save-and-test}

**[!UICONTROL Save & Test]** performs **initial SSH host key enrollment only**. It is conservative by design and does not rotate or overwrite keys that are already enrolled for the connection.

| Enrolled host key state | What Save & Test does |
| --- | --- |
| Host keys not yet enrolled | Scans the bastion host and port, enrolls the host keys, and stores them for this connection |
| Host keys already enrolled | Skips enrollment. Does not overwrite, rotate, or delete existing enrolled keys |
| Enrolled keys missing, empty, or invalid | Does not repair invalid trust material by itself. Use **[!UICONTROL Refresh SSH Host Keys]** or contact Support if errors continue |

After a successful first enrollment, later **[!UICONTROL Save & Test]** runs validate credentials and connection settings but leave enrolled SSH host keys unchanged.

### Expected behavior for Refresh SSH Host Keys {#refresh-ssh-host-keys}

**[!UICONTROL Refresh SSH Host Keys]** updates enrolled SSH host keys when the bastion has changed or when trust material must be repaired. An Admin starts the refresh from the connection in **[!UICONTROL Data]** > **[!UICONTROL Connections]**.

The refresh runs asynchronously on Adobe infrastructure assigned to your account. The Admin UI returns after the job is queued. It does not run the scan on your workstation.

A refresh **rewrites** enrolled host keys only when one of these conditions is true:

* Enrolled host keys are missing
* The enrolled file is empty
* Enrolled host keys cannot be read
* Enrolled host keys fail validation
* A new scan returns different host key lines than the enrolled file
* Fingerprints from the scan and enrolled file do not match

If enrolled keys are current and valid, the refresh completes without changing them.

>[!TIP]
>
>Run **[!UICONTROL Refresh SSH Host Keys]** after your team rotates SSH host keys on the bastion, changes the bastion hostname or IP, or replaces the SSH endpoint. Wait a few minutes, then run **[!UICONTROL Save & Test]** to confirm the connection.

### Expected behavior during account migration {#migration}

Adobe may move your [!DNL Commerce Intelligence] account between data servers during maintenance or scaling. Enrolled SSH host keys are copied to the destination so strict verification continues to work after the move.

| Situation | Expected result |
| --- | --- |
| Host keys already enrolled in the current layout | Keys are copied to the destination. **[!UICONTROL Save & Test]** skips re-enrollment and does not overwrite them |
| Only legacy enrolled key storage exists on the source | Keys are migrated into the current per-connection layout on the destination |
| After migration completes | Run **[!UICONTROL Save & Test]**. Enrollment should be skipped if keys were copied successfully |
| Host keys still fail after migration | An Admin should run **[!UICONTROL Refresh SSH Host Keys]** to repair missing or invalid trust material |

You do not manage enrolled host key files directly. Adobe Support handles migration issues that persist after **[!UICONTROL Save & Test]** and **[!UICONTROL Refresh SSH Host Keys]**.

### SSH host key error messages {#ssh-host-key-errors}

Connection status shows a single user-friendly SSH host key message. Raw OpenSSH errors are not shown in the dashboard.

The following table maps common messages to likely causes and customer actions.

| Message or status | What it means | Possible causes | What you should do |
| --- | --- | --- | --- |
| SSH host key verification failed | The bastion host key does not match enrolled keys, or trust material is unusable | SSH host keys rotated on the bastion; bastion hostname, IP, or port changed; enrolled keys missing, empty, invalid, or unreadable | Confirm **Remote Address** and **SSH Port** on the connection. Ask your infrastructure team whether bastion host keys changed. An Admin runs **[!UICONTROL Refresh SSH Host Keys]**, waits a few minutes, then runs **[!UICONTROL Save & Test]** |
| SSH host keys could not be enrolled | **[!UICONTROL Save & Test]** could not scan or store bastion host keys | Bastion unreachable from Adobe infrastructure; DNS failure; firewall blocks [!DNL Commerce Intelligence] IP addresses; wrong **Remote Address** or **SSH Port**; `ssh-keyscan` failure on the bastion | Verify firewall allowlisting (see [Allow access to the [!DNL Commerce Intelligence] IP address](#allowlist)). Confirm the bastion is up and accepts SSH on the configured port. Correct connection fields and run **[!UICONTROL Save & Test]** again |
| SSH host keys are missing or invalid | Strict verification blocked the tunnel because enrolled trust material is absent or corrupt | First connection never completed enrollment; prior refresh failed; migration did not copy keys; filesystem or permission issue on Adobe infrastructure | An Admin runs **[!UICONTROL Refresh SSH Host Keys]**, then **[!UICONTROL Save & Test]**. If the error persists, contact Support |
| Refresh SSH host keys could not be completed | The refresh job did not update enrolled keys | Replication worker not processing jobs; network, DNS, or scan failure during refresh; permission issue on Adobe infrastructure | Wait several minutes and run **[!UICONTROL Refresh SSH Host Keys]** again. Confirm bastion reachability and allowlisting. Contact Support if the connection still fails after two refresh attempts |

### Troubleshooting checklist {#troubleshooting}

1. Confirm **Remote Address**, **SSH Port**, and Linux user settings match your bastion.
1. Confirm your firewall allows the [!DNL Commerce Intelligence] IP addresses listed in [Allow access to the [!DNL Commerce Intelligence] IP address](#allowlist).
1. Ask your infrastructure team whether SSH host keys on the bastion changed recently.
1. Run **[!UICONTROL Save & Test]** to validate settings and enroll keys if none exist yet.
1. Ask an Admin to run **[!UICONTROL Refresh SSH Host Keys]**, wait a few minutes, then run **[!UICONTROL Save & Test]** again.
1. If the connection still shows an SSH host key error, use **[!UICONTROL Contact Support]** on the connection page (or your account support channel).

### When to contact Adobe Support {#contact-support}

Contact Support when:

* SSH host key errors continue after an Admin runs **[!UICONTROL Refresh SSH Host Keys]** twice and **[!UICONTROL Save & Test]** still fails
* **[!UICONTROL Refresh SSH Host Keys]** never completes or the connection status does not change after 15–30 minutes
* Errors began immediately after Adobe notified you of account migration or data server maintenance
* Bastion settings and firewall allowlisting are correct, your team has not rotated host keys, and you still cannot connect
* You need an Admin to run **[!UICONTROL Refresh SSH Host Keys]** but no Admin is available on the account

Include the connection name, approximate time of the last **[!UICONTROL Save & Test]** or refresh attempt, and whether bastion host keys changed recently. Do not send private keys or passphrases.

## Related {#related}

* [Reauthenticating integrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)

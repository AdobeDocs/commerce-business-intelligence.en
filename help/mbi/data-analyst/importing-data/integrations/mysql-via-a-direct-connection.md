---
title: Connecting MySQL via a direct connection
description: Learn how to connect [!DNL MongoDB] via direct connection.
exl-id: 53765844-c9bb-4a16-b00c-ce9672f87415
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/HkKVLKV9RpLIWN-YY5GggdnlHeBB2Xg9odAbSZklHGE
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
# Connect [!DNL MySQL] via direct connection

## In this topic

* [Allow access to the [!DNL Commerce Intelligence] IP address](#allowlist)
* [Create a [!DNL MySQL] user for [!DNL Commerce Intelligence]](#steptwo)
* [Enter connection info into [!DNL Commerce Intelligence]](#stepthree)

## Jump to

* [[!DNL MySQL] via `SSH tunnel`](../integrations/mysql-via-ssh-tunnel.md)
* [[!DNL MySQL] via [!DNL cPanel]](../integrations/mysql-via-cpanel.md)

>[!NOTE]
>
>[!DNL Adobe] recommends you use [SSH](../integrations/mysql-via-ssh-tunnel.md) or some other form of encryption to secure your data! If this is not an option, you can still directly connect [!DNL Commerce Intelligence] to your database using the instructions in this topic.

This topic walks you through directly connecting your [!DNL MySQL] database to [!DNL Commerce Intelligence]. These settings can also be used with [!DNL Adobe Commerce] or any other eCommerce databases that use MySQL.

## Allow access to the [!DNL Commerce Intelligence] IP addresses {#allowlist}

For the connection to be successful, you must configure your firewall to allow access from your IP addresses. They are `54.88.76.97` and `34.250.211.151`, but it is also on the [!DNL MySQL] credentials page:

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## Create a [!DNL MySQL] user for [!DNL Commerce Intelligence]

The simplest way to create a `MySQL` user for [!DNL Commerce Intelligence] is to execute the following query when logged into `MySQL` with `GRANT` privileges. Replace `Commerce Intelligence IP Address` with the [!DNL Commerce Intelligence] IP address and replace `secure password` with a secure password of your choice:

```sql
    GRANT SELECT ON *.* TO 'magentobi'@'<Commerce Intelligence IP address>' IDENTIFIED BY '<secure password>';
```

To restrict this user from accessing data in specific databases, tables, or columns, you can instead run `GRANT` queries that only allow access to the data you permit.

**Rerun the GRANT query for all required IPs using the same user and password.**

## Enter connection info in Commerce Intelligence

To wrap things up, you need to enter the connection and user info into [!DNL Commerce Intelligence]. Did you leave the [!DNL MySQL] credentials page open? If not, go to **[!UICONTROL Data** > **Connections]** and click **[!UICONTROL Add New Data Source]**, then click the [!DNL MySQL] icon. Do not forget to change the `Encrypted` toggle to `Yes`.

Enter the following info into this page, starting with the `Database Connection` section:

* `Connection Nickname`: Enter a name for the integration (for example, Ecommerce Store)
* `Username`: The username for the [!DNL Commerce Intelligence] [!DNL MySQL] user
* `Password`: The password for the [!DNL Commerce Intelligence] [!DNL MySQL] user
* `Port`: MySQL's port on your server (`3306` by default)
* `Host`: By default, this is localhost. In general, it is the bind-address value for your [!DNL MySQL] server, which by default is `127.0.0.1 (localhost)`, but could also be some local network address (for example, `192.168.0.1`) or your server's public IP address.

   The value can be found in your `my.cnf` file (located at `/etc/my.cnf`) underneath the line that reads `\[mysqld\]`. If the bind-address line is commented out in that file, your server is secured from outside connection attempts.

When you are finished, click **[!UICONTROL Save & Test]** to complete the setup.

## Related documentation

* [Reauthenticating integrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)

---
title: Activate your [!DNL Adobe Commerce Intelligence] Account
description: Learn who to contact to activate your [!DNL Commerce Intelligence] account.
exl-id: 0efac7b4-2457-48c7-947a-d2776b90a1dd
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
---
# Activate your [!DNL Commerce Intelligence] Account for On-Premise and Starter Subscriptions

To activate [!DNL Commerce Intelligence] for on-premise subscriptions, first create a [!DNL Commerce Intelligence] account, enter your settings information, then connect [!DNL Commerce Intelligence] to your [!DNL Commerce] database. <!-- For information about activation in `Cloud Starter` projects, see [Activating your [!DNL Commerce Intelligence] Account for `Cloud Starter` Subscriptions](../getting-started/cloud-activation.md).-->

## Create your [!DNL Commerce Intelligence] account

To create your account, contact your Adobe Account Team or Customer Technical Advisor.

## Create your password

After your account has been created, check your email for an account notification email from [!DNL The Magento BI Team@rjmetrics.com]. Use the link provided in the email to access your [!DNL Commerce Intelligence] account and create your password. Go to your inbox and verify your email address. 

If you did not receive an email, [contact support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).

   ![Create password screen for new Commerce Intelligence account](../assets/create-account-4.png)

## Set your store preferences

   Before you configure the database connection, complete the store information form. This information is required to complete the **[!UICONTROL Connect your Database]** setup.

   ![Store information form with business name, currency, and timezone fields](../assets/create-account-6.png)

## Add [!DNL Commerce Intelligence] users

After you set your password and log into [!DNL Commerce Intelligence], you can add other users to your [!DNL Commerce Intelligence] account. When adding users, add admin users with appropriate permissions to complete the activation process.

   ![Add user form with email address and permission level fields](../assets/create-account-5.png)

## Create a dedicated [!DNL Commerce Intelligence] user in the [!DNL Commerce] admin

To use [!DNL Commerce Intelligence], you must add a permanent and dedicated user to the [!DNL Commerce] project. This dedicated user serves as a permanent connection to [!DNL Commerce] that enables the fetch and transfer of new data to the account's [!DNL Commerce Intelligence] Data Warehouse.

Configuring a dedicated [!DNL Commerce Intelligence] user ensures that the account is not deactivated or deleted, thus stopping the [!DNL Commerce Intelligence] connection.


>[!NOTE]
>
>Adobe encourages using an account name that indicate its permanent status (e.g., ACI-dedicated, ACI-database-connector, and so forth).

After you created the dedicated user for [!DNL Commerce Intelligence] in the Admin, add the same user to the primary environment of the [!DNL Commerce] project with a **[!UICONTROL Master]** setting of `Contributor`.

   ![Commerce add user interface with role set to Contributor](../assets/commerce-add-user-settings.png)

## Get your Commerce Intelligence SSH keys

   1. On the [!UICONTROL Connect your database] page for [!DNL Commerce Intelligence] setup,  scroll down and select **[!UICONTROL Encryption settings]**.

   1. For **Encryption Type**, select `SSH Tunnel`.

   1. From the drop-down, copy the public key that is provided.

      ![Encryption settings page showing SSH Tunnel type and public key field](../assets/encryption-setting-new-account.png)

## Add your public key to the [!DNL Commerce Intelligence]

   1. From the [!DNL Commerce Admin], sign in using the login information for the [!DNL Commerce Intelligence] user you just created.

   1. Select the **Account Settings** tab.

   1. Scroll down and expand the **[!UICONTROL SSH Keys]** drop-down. Then, select **[!UICONTROL Add a public key]**.

       ![Account settings page with SSH Keys section and Add a public key button](../assets/add-public-key.png)

   1. Paste the public key that you copied in the [!DNL Encryption Type] step above.

       ![Add public key form with key text field and Submit button](../assets/paste-public-key.png)

## Provide [!DNL Commerce Intelligence] Essentials `MySQL` credentials

   1. Update your `.magento/services.yaml`.

      ![Code showing MySQL service configuration in services.yaml file](../assets/update-magento-services-yaml.png)

   1. Update your `.magento.app.yaml`.

      ![Code showing database relationships configuration in app.yaml file](../assets/magento-app-yaml-relationships.png)

## Get database connection information

Get the database connection information to the [!DNL Commerce] database to [!DNL Commerce Intelligence]

   1. Run the following to get your information.

        `echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 --decode | json_pp`

   1. Review the database information, which should look similar to the following example.

      ![JSON output showing database connection credentials including host, port, and username](../assets/example-database-information.png)

## Connect [!DNL Commerce Intelligence] to your [!DNL Commerce] database using an encrypted connection

>[!NOTE]
>
>Adobe strongly recommends that you use an [`SSH tunnel`](../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md) tunnel to make the database connection. However, if this method is not an option, you can still link [!DNL Commerce Intelligence] to your database using a [`direct connection`](../data-analyst/importing-data/integrations/mysql-via-a-direct-connection.md).

Enter your [!DNL Commerce Intelligence] information in the [!UICONTROL Connect your Magento Database] screen.

![Connect your database form with fields for integration name, host, port, username, password, and database name](../assets/connect-magento-db.png)

**Inputs:**

[!UICONTROL Integration Name]:  [choose a name for your [!DNL Commerce Intelligence] instance]

[!UICONTROL Host]: `mbi.internal`

[!UICONTROL Port]: `3306`

[!UICONTROL Username]: `mbi`

[!UICONTROL Password]: [input password displayed in the previous section]

[!UICONTROL Database Name]: `main`

[!UICONTROL Table Prefixes]: [leave blank if there are no table prefixes]

## Set your [!UICONTROL **Time Zone**] settings

   ![Time zone settings form with database timezone and desired timezone dropdown fields](../assets/time-zone-settings.png)

   **Inputs:**

   [!UICONTROL Database Timezone]: `UTC`

   [!UICONTROL Desired Timezone]: [choose the time zone for which you want your data to display]

## Get your encryption settings information

The project UI provides an SSH access string. This string can be used for gathering the information needed for the [!UICONTROL **Remote Address**] and [!UICONTROL **Username**]. Use the SSH Access string by selecting the access site button on the Master branch of the Project UI. Then, find your [!UICONTROL User Name] and [!UICONTROL Remote Address] as shown below.

![Project UI showing SSH access information with username and remote address](../assets/master-branch-settings.png)

## Input your [!DNL Encryption] settings

![Encryption settings form with fields for encryption type, remote address, username, and port](../assets/encryption-settings-2.png)

**Inputs:**

[!UICONTROL Encryption Type]: `SSH Tunnel`

[!UICONTROL Remote Address]: `ssh.us-3.magento.cloud`  [from the previous step]

[!UICONTROL Username]: `vfbfui4vmfez6-master-7rqtwti—mymagento`  [from the previous step] 

[!UICONTROL Port]: `22`

## Save your integration.

After completing the configuration steps, apply the changes by selecting [!UICONTROL **Save Integration**].

You have now successfully connected your [!DNL Commerce] database to your [!DNL Commerce Intelligence] account.

>[!NOTE]
>
>If you are a [!DNL Adobe Commerce Intelligence Pro] customer, contact your Customer Success Manager or Customer Technical Advisor to coordinate the next steps.

After you complete the configuration, [sign in](../getting-started/sign-in.md) to your [!DNL Commerce Intelligence] account.

<!---# Activate your [!DNL Commerce Intelligence] Account

To activate [!DNL Commerce Intelligence] for on-premise or `Cloud Pro` subscriptions, [contact support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

>[!NOTE]
>
>Adobe no longer supports new `Cloud Starter` subscriptions.--->

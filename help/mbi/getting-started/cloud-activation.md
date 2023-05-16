---
title: Activate your Commerce Intelligence Account for Cloud Starter Subscriptions
description: Learn how to activate Commerce Intelligence for Cloud Starter projects.
exl-id: 172439ee-fa1d-4872-b6a9-c61a212a7cbe

redirect_to:
  - https://experienceleague.adobe.com/docs/commerce-business-intelligence/mbi/start/onpremise-activation.html
---
<!---# Activate your [!DNL Commerce Intelligence] Account for `Cloud Starter` Subscriptions

To activate [!DNL Commerce Intelligence] for `Cloud Starter` projects, first create an [!DNL Commerce Intelligence] account, then create a `SSH` key, then finally connect to your Commerce database. See [activating on-premise subscriptions](../getting-started/onpremise-activation.md).

>[!NOTE]
>
>For help with activation [!DNL Commerce Intelligence] for `Cloud Pro` projects, contact your Adobe Account Team or Customer Technical Advisor.

1. Create your [!DNL Commerce Intelligence] Account.

    - Go to [Adobe Commerce account login](https://account.magento.com/customer/account/login)

    - Go to **[!UICONTROL My Account** > **My [!DNL Commerce Intelligence] Instances]**.

    - Click **[!UICONTROL Create Instance]**. If you do not see this button, contact your Adobe Account Team or Customer Technical Advisor.

    - Select your `Cloud Starter` subscription. If you only have a `cloud starter` subscription, this is the default selection.

    - Click **[!UICONTROL Continue]**.

    - Input your information to create your account.

     ![](../assets/create-account-2.png)

    - Go to your inbox and verify your email address.

    ![](../assets/create-account-3.png)

    - Create your password.

    ![](../assets/create-account-4.png)

    - After creating your account, you can add users to your new account. Technical admins can now be added to carry out the following steps.

     ![](../assets/create-account-5.png)

1. Input information about your store to set your preferences.

    ![](../assets/create-account-6.png)

    Gather some information before you can connect your database for the third step in the onboarding flow. You complete the `Connect your database` page in Step 9.

1. Create dedicated [!DNL Commerce Intelligence] User.

    - Create a user in your [Adobe Commerce account](https://account.magento.com/customer/account/login).

    - _Why a new user?_ [!DNL Commerce Intelligence] needs a user added to the project to continuously fetch new data to be transferred to the account's [!DNL Commerce Intelligence] Data Warehouse. This user serves as that connection. Adding this user to the project is covered in Step 4.

    - The reason for having a dedicated [!DNL Commerce Intelligence] user is to prevent the added user from inadvertently being deactivated or deleted and stopping the [!DNL Commerce Intelligence] connection.

1. Add the newly created user to the project's primary environment as a `Contributor`.

    ![](../assets/create-account-7.png)

1. Get your [!DNL Commerce Intelligence] `SSH` keys.

    - Go to the `Connect your database` page of the [!DNL Commerce Intelligence] setup user interface and scroll down to `Encryption settings`.

    - For the `Encryption Type` field, choose `SSH Tunnel`.

    - From the dropdown, you can copy and paste the provided [!DNL Commerce Intelligence] `Public Key`.

    ![](../assets/create-account-8.png)

1. Add your new [!DNL Commerce Intelligence] `Public key` to the [!DNL Commerce Intelligence] user created in Step 5.

    - Go to [your cloud Adobe Commerce account](https://account.magento.com/cloud/customer/login/). Sign in with your account login information for the new [!DNL Commerce Intelligence] user created. Then go to the `Account Settings` tab.

    - Scroll down the page and expand the dropdown for `SSH` keys. Then click **[!UICONTROL Add a public key]**.

    ![](../assets/create-account-9.png)

    - Add the [!DNL Commerce Intelligence] `SSH Public Key` from above.

    ![](../assets/create-account-10.png)

1. Provide [!DNL Commerce Intelligence] [!DNL MySQL] credentials.

    - Update your `.magento/services.yaml`

    ```sql
    mysql:
        type: mysql:10.0
        disk: 2048
        configuration:
            schemas:
                - main
            endpoints:
                mysql:
                    default_schema: main
                    privileges:
                        main: admin
                mbi:
                    default_schema: main
                    privileges:
                        main: ro
    ```

    - Update your `.magento.app.yaml`

    ```sql
            relationships:
                database: "mysql:mysql"
                mbi: "mysql:mbi"
                redis: "redis:redis"
    ```

1. Get information for connecting your database to [!DNL Commerce Intelligence].

    Run
    `echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 --decode | json_pp`

    to get information on connecting your database.

    You should receive information similar to the output below:

    ```json
            "mbi" : [
                  {
                     "scheme" : "mysql",
                     "rel" : "mbi",
                     "cluster" : "vfbfui4vmfez6-master-7rqtwti",
                     "query" : {
                        "is_master" : true
                     },
                     "ip" : "169.254.169.143",
                     "path" : "main",
                     "host" : "[!DNL Commerce Intelligence].internal",
                     "hostname" : "3m7xizydbomhnulyglx2ku4wpq.mysql.service._.magentosite.cloud",
                     "username" : "mbi",
                     "service" : "mysql",
                     "port" : 3306,
                     "password" : "[password]"
                  }
               ],
    ```

1. Connect your Commerce Database

   ![](../assets/create-account-11.png)

    - `Integration Name`: [Choose a name for your integration.]

    - `Host`: `[!DNL Commerce Intelligence].internal`

    - `Port`: `3306`

    - `Username`: `mbi`

    - `Password`: [input password provided in the output for Step 8.]

    - `Database Name`: `main`

    - `Table Prefixes`: [leave blank if there are no table prefixes]

1. Set your Timezone Settings.

    ![Inputs](../assets/create-account-12.png)

     - `Database`: `Timezone: UTC`

     - `Desired Timezone`: [Choose the time zone for which you want your data to display in.]

1. Get information for your encryption settings.

    - The project UI provides an `SSH` access string. This string can be used for gathering the information needed for `Remote Address` and `Username` in setting up your `Encryption` settings. Use the `SSH Access` string found by clicking the access site button on your Primary branch of your Project UI and find your `User Name` and `Remote Address` as shown below.

    ![](../assets/create-account-13.png)

    ![](../assets/create-account-14.png)

1. Input information for your `Encryption` settings

    ![](../assets/create-account-15.png)

    **Inputs**

     - `Encryption Type`: `SSH Tunnel`

     - `Remote Address`: `ssh.us-3.magento.cloud`

     - `Username`: `vfbfui4vmfez6-master-7rqtwti--mymagento`

     - `Port`: `22`

1. Click **[!UICONTROL Save Integration]**.

1. You have now successfully connected to your [!DNL Commerce Intelligence] account.

1. After you have successfully connected [!DNL Commerce Intelligence] to your Commerce database, contact your Adobe Account Team to coordinate the next steps, such as setting up integrations and other configuration steps.

1. When you finish configuration, you can [sign in](../getting-started/sign-in.md) to your [!DNL Commerce Intelligence] account.--->

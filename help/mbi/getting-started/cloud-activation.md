---
title: Activating your MBI Account for Cloud Starter Subscriptions
zendesk_id: 360016504752

---

To activate MBI for Cloud Starter projects, first create a MBI account, then create a SSH key, then finally connect to your Magento database. Click [here](../../getting-started/onpremise-activation.md) for activating on-premise subscriptions.

{:.bs-callout-info}
For help activating MBI for Cloud Pro projects, contact your Magento Customer Success Manager or Customer Technical Advisor.

1. Create your MBI Account.

    - Go to [https://account.magento.com/customer/account/login](https://account.magento.com/customer/account/login)

    - Go to **My Account** → **My MBI Instances**.

    - Click the **Create Instance**. If you do not see this button, contact your Customer Success Manager or Customer Technical Advisor.

    - Select your Cloud Starter subscription. If you only have a cloud starter subscription this will automatically be selected.

    - Click **Continue**.

    - Input your information to create your account.

     ![Picture2.png](../../assets/Picture2.png)

    - Go to your inbox and verify your email address.

    ![Picture3.png](../../assets/Picture3.png)

    - Create your password.

    ![Picture4.png](../../assets/Picture4.png)

    - After creating your account you will then have the option to add users to your new account. Technical admins can now be added to carry out the following steps.

     ![Picture5.png](../../assets/Picture5.png)

1. Input information about your store to set your preferences.

    ![Picture6.png](../../assets/Picture6.png)

    There is some information you need to gather before you can connect your database for the third step in the onboarding flow. You will be filling in the **Connect your database** page in Step **9**.

1. Create dedicated MBI User.

    - Create a new user on [https://accounts.magento.com](https://accounts.magento.com).

    - _Why a new user?_ MBI needs a user added to the project to continuously fetch new data to be transferred to the account's MBI data warehouse. This user will serve as that connection. Adding this user to the project will come in Step **4**.

    - The reason for having a dedicated MBI user is to prevent the added user from inadvertently being deactivated or deleted and stopping the MBI connection.

1. Add the newly created user to the project's primary environment as a `Contributor`.

    ![Picture7.png](../../assets/Picture7.png)

1. Get your MBI SSH keys.

    - Go to the **Connect your database** page of the MBI set up user interface and scroll down to **Encryption settings**.

    - For the field **Encryption Type** chose **SSH Tunnel**.

    - From the dropdown, you can copy and paste the provided MBI Public Key.

    ![Picture8.png](../../assets/Picture8.png)

1. Add your new MBI Public key to the MBI user created in Step **5**.

    - Go to [https://accounts.magento.cloud/](https://accounts.magento.cloud/). Sign in with your account log in information for the new MBI user created. Then go to the **Account Settings** tab.

    - Scroll down the page and expand the dropdown for SSH keys. Then click **Add a public key**.

    ![Picture9.png](../../assets/Picture9.png)

    - Add the MBI SSH Public Key from above.

    ![Picture10.png](../../assets/Picture10.png)

1. Provide MBI MySQL credentials.

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

1. Get information for connecting your database to MBI.

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
                     "host" : "mbi.internal",
                     "hostname" : "3m7xizydbomhnulyglx2ku4wpq.mysql.service._.magentosite.cloud",
                     "username" : "mbi",
                     "service" : "mysql",
                     "port" : 3306,
                     "password" : "[password]"
                  }
               ],
    ```

1. Connect your Magento Database

   ![Picture11.png](../../assets/Picture11.png)*Inputs*

    - Integration Name: [Choose a name for your integration.]

    - Host: `mbi.internal`

    - Port: `3306`

    - Username: `mbi`

    - Password: [input password provided in Step **8**'s output.]

    - Database Name: `main`

    - Table Prefixes: [leave blank if there are no table prefixes]

1. Set your Timezone Settings.

    ![Picture12.png](../../assets/Picture12.png)*Inputs*

     - Database: `Timezone: UTC`

     - Desired Timezone: [Choose the time zone you want your data to display in.]

1. Get information for your encryption settings.

    - The project UI provides an SSH access string. This string can be used for gathering the information needed for the **Remote Address** and **Username** in setting up your **Encryption settings**.  Use the SSH Access string found by clicking the access site button on your Master branch of your Project UI and find your **User Name** and **Remote Address** as shown below.

    ![Picture13.png](../../assets/Picture13.png)

    ![Picture14.png](../../assets/Picture14.png)

1. Input information for your Encryption Settings

    ![Picture15.png](../../assets/Picture15.png)

    **Inputs**

     - Encryption Type: `SSH Tunnel`

     - Remote Address: `ssh.us-3.magento.cloud`

     - Username: `vfbfui4vmfez6-master-7rqtwti--mymagento`

     - Port: `22`

1. Click **Save Integration**.

1. You have now successfully connected to your MBI account.

1. After you have successfully connected MBI to your Commerce database, contact your Customer Success Manager to coordinate the next steps, such as setting up integrations and other configuration steps.

1. When you finish configuration, you can [sign in](../../getting-started/sign-in.md) to your MBI account.

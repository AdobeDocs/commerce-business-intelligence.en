---
title: Activating your [!DNL MBI] Account for On-Premise Subscriptions
description: Learn about activating your [!DNL MBI] account for On-Premise Subscriptions.
exl-id: 0efac7b4-2457-48c7-947a-d2776b90a1dd
---
# Activate your [!DNL MBI] Account for On-Premise Subscriptions

To activate [!DNL MBI] for on-premise subscriptions, first create a [!DNL MBI] account, then connect [!DNL MBI] to your Commerce database. For information about activation in `Cloud Starter` projects, see [Activating your [!DNL MBI] Account for `Cloud Starter` Subscriptions](../getting-started/cloud-activation.md).

1. Create your [!DNL MBI] Account.

    -  Go to your [Adobe Commerce account login](https://account.magento.com/customer/account/login)

    -  Go to **[!UICONTROL My Account** > **My [!DNL MBI] Instances]**.

    -  Click **[!UICONTROL Create Instance]**. If you do not see this button, contact your Customer Success Manager or Customer Technical Advisor.

    -  Enter your information to create your account.

     ![](../assets/create-account-2.png)

    -  Go to your inbox and verify your email address. If you did not receive an email, [contact support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).

    -  Create your password.

    ![](../assets/create-account-4.png)

    -  After you create your account, you have the option to add users to your new account. Technical admins can now be added to carry out the following steps.

     ![](../assets/create-account-5.png)

1. Enter information about your store to set your preferences.

    ![](../assets/create-account-6.png)

1. Connect [!DNL MBI] to your Commerce database using an encrypted connection.

   Commerce strongly recommends you connect using an [`SSH tunnel`](../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md). However, if this is not an option, you can still link [!DNL MBI] to your database using a [`direct connection`](../data-analyst/importing-data/integrations/mysql-via-a-direct-connection.md).

1. After you have successfully connected [!DNL MBI] to your Commerce database, contact your Customer Success Manager to coordinate the next steps, such as setting up integrations and other configuration steps.

1. When you finish configuration, you can [sign in](../getting-started/sign-in.md) to your [!DNL MBI] account.

---
title: Connect Google ECommerce
description: Learn about your most valued referral channels.
exl-id: c80f52f3-894a-4084-8c0e-aee618ed77f5
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
---
# Connect [!DNL Google ECommerce]

>[!NOTE]
>
>Requires [Admin permissions](../../../administrator/user-management/user-management.md).

![](../../../assets/google-ecommerce-logo.png)

You have steady flow of traffic and orders, which means you are effectively reaching and acquiring customers. But what are your most valuable referral channels? What is the average lifetime value of customers acquired from one source versus another? By connecting your order referral source data from [!DNL Google ECommerce] to [!DNL Commerce Intelligence], you can build analyses that help you identify your [most valuable marketing channels](../../../data-analyst/analysis/most-value-source-channel.md).

Get started by entering your [!DNL Google ECommerce] credentials into [!DNL Commerce Intelligence]:

1. Go to the `Connections` page under **[!UICONTROL Admin** > **Connections]**.

1. Click **[!UICONTROL Add a New Source]**, located on the right side of the screen above the `Data Sources` table.

1. Click the [!DNL Google ECommerce] icon. This opens the [!DNL Google ECommerce] credentials page.

1. Enter your [!DNL Google Analytics] credentials. At completion of the authorization process, you are redirected back to [!DNL Commerce Intelligence].

1. A list of profile IDs display. Check the profiles that you want to connect to [!DNL Commerce Intelligence].

     If you have multiple profiles and need some help identifying which is which, refer to the **Connecting Multiple [!DNL Google Analytics] profiles section below.

     ![](../../../assets/conn-mult-ga-profiles.png)<!--{: width="500"}-->

1. Changes are saved automatically, so click **[!UICONTROL Back to Connections]** when you are finished.

## Connecting multiple [!DNL Google Analytics] profiles to [!DNL Commerce Intelligence]

You may have multiple websites connected to a single [!DNL Google Analytics] account, identified by their own [!DNL Google Analytics] profile ID. In this case, you have the option of including all your profile IDs in [!DNL Commerce Intelligence]. Check the profile IDs you would like to include during the profile selection step.

To identify a particular website's [!DNL Google Analytics] Profile ID:

1. Log into [!DNL Google Analytics].
1. Go to the particular website's [!DNL Google Analytics] dashboard.
1. Look at the URL - the Profile ID corresponds to the eight numbers following `p` at the end of the line.

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## Disconnecting [!DNL Google ECommerce] from [!DNL Commerce Intelligence] {#disconnect}

1. Visit your [!DNL Google Analytics] [account settings](https://www.google.com/account/about/?hl=en) page.
1. Under the `Security` section, click **[!UICONTROL edit]** next to `Authorizing` applications and sites.
1. Click **[!UICONTROL revoke access]** next to [!DNL Commerce Intelligence].

## Related:

* [Expected [!DNL Google ECommerce] data](../integrations/google-ecommerce-data.md)
* [Reauthenticating integrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [Setting up [!DNL Google ECommerce] tracking](https://support.google.com/analytics/answer/1009612?hl=en)
* [Discover your most valuable acquisition sources and channels](../../analysis/most-value-source-channel.md)
* [Increase ROI on your advertising campaigns](../../analysis/roi-ad-camp.md)

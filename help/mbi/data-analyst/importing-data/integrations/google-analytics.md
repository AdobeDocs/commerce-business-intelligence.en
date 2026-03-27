---
title: Connect Google Analytics
description: Learn to connect Google Analytics with [!DNL Commerce Intelligence].
exl-id: 10e813f1-0306-4bdd-8222-e6364ac624de
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
---
# Connect [!DNL Google Analytics]

>[!NOTE]
>
>Requires [Admin permissions](../../../administrator/user-management/user-management.md).

![Google Analytics logo](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] is the most widely used web analytics service on the internet. Implementing [!DNL Google Analytics] on your website allows you to track how visitors use your site, what content is attractive, where visitors exit, and more. Analyzing these metrics in [!DNL Commerce Intelligence], alongside other pieces of data, improves your site's overall health and usability.

Get started by entering your [!DNL Google Analytics] credentials into [!DNL Commerce Intelligence]:

1. Go to **[!UICONTROL Manage Data** > **Integrations]**.

1. Click **[!UICONTROL Add Integration]**, located on the right side of the screen.

1. Click the [!DNL Google Analytics] icon. This opens the [!DNL Google Analytics] credentials page.

1. Enter your [!DNL Google Analytics] credentials. At completion of the authorization process, you are redirected back to [!DNL Commerce Intelligence].

1. A list of profile IDs display. Check the profiles that you want to connect to [!DNL Commerce Intelligence]. If you have multiple profiles and need some help identifying which is which, refer to the Connecting Multiple [!DNL Google Analytics] profiles section below.

     ![Google Analytics Admin page showing profile ID in URL](../../../assets/list-profile-id.png)<!--{: width="600px"}-->

1. Changes are saved automatically, so click **Back to Connections** when you are done.

## Connecting multiple [!DNL Google Analytics] profiles

You may have multiple websites connected to a single [!DNL Google Analytics] account, identified by their own [!DNL Google Analytics] profile ID. In this case, you have the option of including all your profile IDs in [!DNL Commerce Intelligence]. Check the profile IDs you would like to include during the profile selection step.

To identify a particular website's [!DNL Google Analytics] Profile ID:

1. Log into [!DNL Google Analytics]
1. Go to the particular website's [!DNL Google Analytics] dashboard
1. Look at the URL - the Profile ID corresponds to the eight numbers following `p` at the end of the line:

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## Disconnecting [!DNL Google Analytics] from [!DNL Commerce Intelligence] {#disconnect}

1. Visit your [!DNL Google Analytics] [account settings](https://accounts.google.com/) page.
1. Under the `Security` section,  and click **[!UICONTROL edit]** next to `Authorizing` applications and sites.
1. Click **[!UICONTROL revoke access]** next to [!DNL Commerce Intelligence].

## Related:

* [Reauthenticating integrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [Connecting [!DNL Google Adwords]](../integrations/google-adwords.md)
* [Analyzing website activity and customer conversion rates](../../analysis/web-act-cust-conversion.md)
* [Track user acquisition data using [!DNL Google Analytics] cookies](../../analysis/google-track-user-acq.md)

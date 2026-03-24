---
title: Connect Google Analytics Warehoused
description: Learn to track how visitors use your site, what content is attractive, where visitors exit, and more.
exl-id: b9879399-9e1a-4f36-b510-8426ebc83aeb
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/fmI-RG3Ba7s--6-Qve8xzcBLAKcbAqfaMAb7hNiKciU
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
    internal-label: Security
  - id: f42e0a1a-0d79-488d-a83f-f2c30672b137
    internal-label: Reporting
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
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
    internal-label: Reporting
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
---
# Connect [!DNL Google Analytics Warehoused]

>[!NOTE]
>
>Requires [Admin permissions](../../../administrator/user-management/user-management.md).

![Google Analytics logo](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] is the most widely used web analytics service on the internet. Implementing [!DNL Google Analytics] on your website allows you to track how visitors use your site, what content is attractive, where visitors exit, and more. [!DNL Google Analytics Warehoused] is a separate integration from your existing [!DNL Google Analytics] integration. It allows for better analysis due to having the [!DNL Google Analytics] data in your Data Warehouse, which is different from the live feed of the existing [!DNL Google Analytics] integration. Analyzing these metrics in [!DNL Commerce Intelligence], alongside other pieces of data, improves your site's overall health and usability.

## Difference between GA Warehoused and Live Integration

The main differentiator is that one integration is stored ([!DNL Google Analytics Warehoused]), and the other is not ([!DNL Google Analytics Live]). In the case of [!DNL Google Analytics Warehoused], this allows for manipulation of your [!DNL Google Analytics] data and gives you the ability to combine [!DNL Google Analytics] and other data sources to create insightful reporting.

Look at [!DNL Google Analytics] ad campaigns for an example of what can be done from a manipulation standpoint. Suppose you had multiple ad campaigns for fourth quarter with different names. The campaigns were a result of a specific marketing initiative. With warehoused data, you can create a column that finds the campaign names in question and returns the fourth quarter initiative name of `Operation Dumbo`.

The combination aspect allows [!DNL Google Analytics] data to be joined to other data in order to conduct analyses. For example, take `Total Time On Site By Ad Campaign` data from [!DNL Google Analytics] and join it up against `Total Spent Per Campaign` data from [!DNL Facebook Ads] to get a complete picture of how much engagement is costing you.

With the [!DNL Google Analytics Live] integration on the other hand, every [!DNL Google Analytics] chart is like a little silo that is not stored in your Data Warehouse.

## Connecting [!DNL Google Analytics Warehoused]

>[!INFO]
>
>[!DNL Google Analytics Warehoused] is a `Premium` Integration. [Contact support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) if you have an interest in adding this integration to your subscription.

1. Go to the `Connections` page under **[!UICONTROL Admin** > **Integrations]**.
1. Click **[!UICONTROL Add an Integration]**, located on the right side.
1. Click the [!DNL Google Analytics Warehoused] icon. This opens the [!DNL Google Analytics] credentials page.
1. Enter your [!DNL Google Analytics] credentials. Upon completion of the authorization process, you are redirected back to [!DNL Commerce Intelligence].
1. A list of profile IDs display. Check the profiles that you want to connect to [!DNL Commerce Intelligence]. If you have multiple profiles and need some help identifying which is which, refer to the Connecting Multiple [!DNL Google Analytics] profiles section below.

## Connecting multiple [!DNL Google Analytics] profiles

You may have multiple websites connected to a single [!DNL Google Analytics] account, identified by their own [!DNL Google Analytics] profile ID. In this case, you have the option of including all your profile IDs in [!DNL Commerce Intelligence]. Check the profile IDs you would like to include during the profile selection step.

To identify a particular website's [!DNL Google Analytics] Profile ID:

1. Log into [!DNL Google Analytics]
1. Go to the particular website's [!DNL Google Analytics] dashboard
1. Look at the URL - the Profile ID corresponds to the eight numbers following `p` at the end of the line 

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## Disconnecting [!DNL Google Analytics Warehoused] from [!DNL Commerce Intelligence] {#disconnect}

1. Visit your [!DNL Google Analytics] [account settings](https://myaccount.google.com/intro) page.
1. Under the `Security` section,  and click **[!UICONTROL edit]** next to `Authorizing` applications and sites.
1. Click **[!UICONTROL revoke access]** next to [!DNL Commerce Intelligence].

## Related documentation

* [Reauthenticating integrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [Connecting [!DNL Google Adwords]](../integrations/google-adwords.md)
* [Analyzing website activity and customer conversion rates](../../analysis/web-act-cust-conversion.md)
* [Track user acquisition data using [!DNL Google Analytics] cookies](../../analysis/google-track-user-acq.md)

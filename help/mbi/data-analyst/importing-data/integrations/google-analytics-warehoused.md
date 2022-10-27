---
title: Connect Google Analytics Warehoused
description: Learn to track how visitors use your site, what content is attractive, where visitors exit, and more.
---
# Connect [!DNL Google Analytics Warehoused]

>[!NOTE]
>
>Requires [Admin permissions](../../../administrator/user-management/user-management.md).

[!DNL Google Analytics] is the most widely-used web analytics service on the internet. Implementing [!DNL Google Analytics] on your website allows you to track how visitors use your site, what content is attractive, where visitors exit, and more. [!DNL Google Analytics Warehoused] is a separate integration from our existing [!DNL Google Analytics] integration. It will allow for better analysis due to having the [!DNL Google Analytics] data in your Data Warehouse, which is different than the live feed of the existing [!DNL Google Analytics] integration. Analyzing these metrics in [!DNL MBI], alongside other pieces of data, will improve your site's overall health and usability.

## Difference between GA Warehoused and Live Integration

The main differentiator is that one integration is stored ([!DNL Google Analytics Warehoused]), and the other is not ([!DNL Google Analytics Live]). In the case of [!DNL Google Analytics Warehoused], this allows for manipulation of your [!DNL Google Analytics] data and gives you the ability to combine [!DNL Google Analytics] and other data sources to create insightful reporting.

Let us look at [!DNL Google Analytics] ad campaigns for an example of what can be done from a manipulation standpoint. Suppose you had multiple ad campaigns for Q4 with different names. The campaigns were a result of a specific marketing initiative. With warehoused data, we can create a new column that finds the campaign names in question and returns the Q4 initiative name of `Operation Dumbo`.

The combination aspect allows [!DNL Google Analytics] data to be joined to other data in order to conduct analyses. For example, take `Total Time On Site By Ad Campaign` data from [!DNL Google Analytics] and join it up against `Total Spent Per Campaign` data from [!DNL Facebook Ads] to get a complete picture of how much engagement is costing you.

With the [!DNL Google Analytics Live] integration on the other hand, every [!DNL Google Analytics] chart is like a little silo that is not stored in your [!DNL MBI] data warehouse.

## Connecting [!DNL Google Analytics Warehoused]

>[!INFO]
>
>[!DNL Google Analytics Warehoused] is a `Premium` Integration. [Contact support](../../../getting-started/support.md) if you have an interest in adding this integration to your subscription.

1. Go to the `Connections` page under **[!UICONTROL Admin** > **Integrations]**.
1. Click **[!UICONTROL Add a Add Integration]**, located on the right side of the screen.
1. Click the [!DNL Google Analytics Warehoused] icon. This will open the [!DNL Google Analytics] credentials page.
1. Enter your [!DNL Google Analytics] credentials. Upon completion of the authorization process, you will be redirected back to [!DNL MBI].
1. A list of profile IDs will display. Check the profiles you want to connect to [!DNL MBI]. If you have multiple profiles and need some help identifying which is which, refer to the Connecting Multiple [!DNL Google Analytics] profiles section below.

## Connecting multiple [!DNL Google Analytics] profiles

You may have multiple websites connected to a single [!DNL Google Analytics] account, identified by their own [!DNL Google Analytics] profile ID. In this case, you will have the option of including all your profile IDs in [!DNL MBI]. Just check the profile IDs you would like to include during the profile selection step.

To identify a particular website's [!DNL Google Analytics] Profile ID:

1. Log into [!DNL Google Analytics]
1. Go to the particular website's [!DNL Google Analytics] dashboard
1. Look at the URL - the Profile ID corresponds to the 8 numbers following `p` at the end of the line 

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## Disconnecting [!DNL Google Analytics Warehoused] from [!DNL MBI] {#disconnect}

1. Visit your [!DNL Google Analytics] [account settings](https://www.google.com/accounts/) page.
1. Under the `Security` section,  and click **[!UICONTROL edit]** next to `Authorizing` applications and sites.
1. Click **[!UICONTROL revoke access]** next to [!DNL MBI].

## Related documentation

* [Reauthenticating integrations](https://support.magento.com/hc/en-us/articles/360016733151)
* [Connecting [!DNL Google Adwords]](../integrations/google-adwords.md)
* [Analyzing website activity and customer conversion rates](../../analysis/web-act-cust-conversion.md)
* [Track user acquisition data using [!DNL Google Analytics] cookies](../../analysis/google-track-user-acq.md)
* [Track user device and browser data using [!DNL Google Analytics] cookies](https://support.magento.com/hc/en-us/articles/360016732911)


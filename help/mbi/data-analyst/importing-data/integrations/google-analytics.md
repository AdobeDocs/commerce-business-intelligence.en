---
title: Connect Google Analytics
description: Learn to connect Google Analytics with [!DNL MBI].
---
# Connect Google Analytics

>[!NOTE]
>
>Requires [Admin permissions.](../../../administrator/user-management/user-management.md)

![](../../../assets/google-analytics-logo.png)

Google Analytics is the most widely-used web analytics service on the internet. Implementing Google Analytics on your website allows you to track how visitors use your site, what content is attractive, where visitors exit, and more. Analyzing these metrics in [!DNL MBI], alongside other pieces of data, will improve your site's overall health and usability.

Let us get started by entering our Google Analytics credentials into MBI:

1. Go to the **Manage Data > Integrations** page.
1. Click **Add Integration**, located on the right side of the screen.
1. Click the Google Analytics icon. This will open the Google Analytics credentials page.
1. Enter your Google Analytics credentials. At completion of the authorization process, you will be redirected back to [!DNL MBI].
1. A list of profile IDs will display. Check the profiles you want to connect to [!DNL MBI]. If you have multiple profiles and need some help identifying which is which, refer to the Connecting Multiple Google Analytics profiles section below.

     ![](../../../assets/list-profile-id.png)<!--{: width="600px"}-->

1. Changes are saved automatically, so click **Back to Connections** when you are done.

## Connecting multiple Google Analytics profiles

You may have multiple websites connected to a single Google Analytics account, identified by their own Google Analytics profile ID. In this case, you will have the option of including all your profile IDs in [!DNL MBI]. Just check the profile IDs you would like to include during the profile selection step.

To identify a particular website's Google Analytics Profile ID:

1. Log into Google Analytics
1. Go to the particular website's Google Analytics dashboard
1. Look at the URL - the Profile ID corresponds to the 8 numbers following "p" at the end of the line:

   www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/

## Disconnecting Google Analytics from [!DNL MBI] {#disconnect}

1. Visit your Google [account settings](https://www.google.com/accounts/) page.
1. Under the Security section,  and click the 'edit' link next to Authorizing applications and sites.
1. Click the 'revoke access' link next to [!DNL MBI].

## Related:

* [Reauthenticating integrations](https://support.magento.com/hc/en-us/articles/360016733151)
* [Connecting Google Adwords](../integrations/google-adwords.md)
* [Analyzing website activity and customer conversion rates](../../analysis/web-act-cust-conversion.md)
* [Track user acquisition data using GA cookies](../../analysis/google-track-user-acq.md)
* [Track user device and browser data using GA cookies](https://support.magento.com/hc/en-us/articles/360016732911)

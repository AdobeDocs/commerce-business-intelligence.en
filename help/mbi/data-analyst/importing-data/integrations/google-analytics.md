---
title: Connecting Google Analytics
zendesk_id: 360016732851
---

{:.bs-callout-info}
[Requires Admin permissions]({% link administrator/user-management/user-management.md %})

![]({% link images/google-analytics-logo.png %})

Google Analytics (GA) is the most widely-used web analytics service on the internet. Implementing GA on your website allows you to track how visitors use your site, what content is attractive, where visitors exit, and more. Analyzing these metrics in Magento BI, alongside other pieces of data, will improve your site\'s overall health and usability.

Let\'s get started by entering our GA credentials into Magento BI:

1. Go to the **Manage Data > Integrations** page.
1. Click the Add Integration button, located on the right side of the screen.
1. Click the Google Analytics icon. This will open the Google Analytics credentials page.
1. Enter your GA credentials. Upon completion of the authorization process, you will be redirected back to Magento BI.
1. A list of profile IDs will display. Check the profiles you want to connect to Magento BI. If you have multiple profiles and need some help identifying which is which, refer to the Connecting Multiple GA profiles section below.

     ![]({% link images/Screen_Shot_2015-11-17_at_11.20.08_AM.png %}){: width="600px"}

1. Changes are saved automatically, so click the Back to Connections button when you\'re done.

## Connecting multiple Google Analytics profiles

You may have multiple websites connected to a single Google Analytics account, identified by their own GA profile ID. In this case, you will have the option of including all your profile IDs in Magento BI. Just check the profile IDs you\'d like to include during the profile selection step.

To identify a particular website\'s Google Analytics Profile ID:

1. Log into Google Analytics
1. Go to the particular website\'s GA dashboard
1. Look at the URL - the Profile ID corresponds to the 8 numbers following \"p\" at the end of the line:

   www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/

## Disconnecting Google Analytics from Magento BI {#disconnect}

1. Visit your Google [account settings](https://www.google.com/accounts/) page.
1. Under the Security section,  and click the \'edit\' link next to Authorizing applications and sites.
1. Click the \'revoke access\' link next to Magento BI.

## Related:

* [Reauthenticating integrations](https://support.magento.com/hc/en-us/articles/360016733151)
* [Connecting Google Adwords]({% link data-analyst/importing-data/integrations/google-adwords.md %})
* [Analyzing website activity and customer conversion rates]({% link data-analyst/analysis/web-act-cust-conversion.md %})
* [Track user acquisition data using GA cookies]({% link data-analyst/analysis/google-track-user-acq.md %})
* [Track user device and browser data using GA cookies](https://support.magento.com/hc/en-us/articles/360016732911)

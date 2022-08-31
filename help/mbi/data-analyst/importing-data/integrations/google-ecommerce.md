---
title: Connecting Google ECommerce
zendesk_id: 360016732951
---

{:.bs-callout-info}
[Requires Admin permissions]({% link administrator/user-management/user-management.md %})

You\'ve got steady flow of traffic and orders, which means you\'re effectively reaching and acquiring customers. But what are your most valuable referral channels? What\'s the average lifetime value of customers acquired from one source versus another? By connecting your order referral source data from Google ECommerce to Magento BI, you can build analyses that will help you identify your [most valuable marketing channels]({% link data-analyst/analysis/most-value-source-channel.md %}).

Let\'s get started by entering our Google ECommerce credentials into Magento BI:

1. Go to the Connections page under **Admin &gt; Connections**.
1. Click the **Add a New Source** button, located on the right side of the screen above the Data Sources table.
1. Click the **Google ECommerce** icon. This will open the Google ECommerce credentials page.
1. Enter your Google Analytics (GA) credentials. Upon completion of the authorization process, you will be redirected back to Magento BI.
1. A list of profile IDs will display. Check the profiles you want to connect to Magento BI.

     If you have multiple profiles and need some help identifying which is which, refer to the **Connecting Multiple GA profiles** section below.

     ![]({% link images/Screen_Shot_2015-11-17_at_12.16.43_PM.png %}){: width="500"}

1. Changes are saved automatically, so just click the **Back to Connections** button when you\'re finished.

## Connecting multiple GA profiles to Magento BI

You may have multiple websites connected to a single GA account, identified by their own GA profile ID. In this case, you will have the option of including all your profile IDs in Magento BI. Just check the profile IDs you\'d like to include during the profile selection step.

To identify a particular website\'s Google Analytics Profile ID:

1. Log into Google Analytics
1. Go to the particular website\'s GA dashboard
1. Look at the URL - the Profile ID corresponds to the 8 numbers following \"p\" at the end of the line: e.g. www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/

## Disconnecting Google ECommerce from Magento BI {#disconnect}

1. Visit your Google [account settings](https://www.google.com/accounts/) page.
1. Under the Security section,  and click the \'edit\' link next to Authorizing applications and sites.
1. Click the \'revoke access\' link next to Magento BI.

## Related:

* [Expected Google ECommerce data]({% link data-analyst/importing-data/integrations/google-ecommerce-data.md %})
* [Reauthenticating integrations](https://support.magento.com/hc/en-us/articles/360016733151)
* [Setting up Google ECommerce tracking](https://support.google.com/analytics/answer/1009612?hl=en)
* [Discover your most valuable acquisition sources and channels]({% link data-analyst/analysis/most-value-source-channel.md %})
* [Increase ROI on your advertising campaigns]({% link data-analyst/analysis/roi-ad-camp.md %})

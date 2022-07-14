---
title: Connecting Google Adwords
zendesk_id: 360016732531
---

{:.bs-callout-info}
[Requires Admin permissions]({% link administrator/user-management/user-management.md %})

![]({% link images/Google_Adwords_logo.png %})

You did your research, you created your ads, you launched your campaign. Now it\'s time to analyze your ad spend data and see if your money is being spent effectively. Using your ad spend data, you can [measure campaign ROI by marrying your advertising cost and the customer lifetime value (CLV)]({% link data-analyst/analysis/roi-ad-camp.md %}) of users acquired from your campaigns.

Let\'s get started by entering our Google Adwords credentials into Magento BI:

1. Go to the Connections page under **Manage Data > Integrations**.
1. Click the **Add Integration** button, located on the upper-right side of the screen.
1. Click the **Google Adwords** icon. This will open the Google Adwords credentials page.
1. Enter your Google Analytics (GA) credentials. Upon completion of the authorization process, you will be redirected back to Magento BI.
1. A list of profile IDs will display. Check the profiles you want to connect to Magento BI.

     ![]({% link images/cnnct-profile.png %}){: width="400"}

1. Changes are saved automatically, so click the **Back to Connections** button when you\'re done.

If you have multiple profiles and need some help identifying which is which, refer to the **Connecting Multiple GA profiles** section below.

## Connecting multiple GA profiles to Magento BI

You may have multiple websites connected to a single GA account, identified by their own GA Profile ID. In this case, you will have the option of including all your Profile IDs in Magento BI. Just check the profile IDs you\'d like to include during the profile selection step.

**To identify a particular website\'s Google Analytics Profile ID:**

1. Log into Google Analytics
1. Go to the particular website\'s GA dashboard
1. Look at the URL - the Profile ID corresponds to the 8 numbers following \"p\" at the end of the line:

     *www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX***

## Disconnecting Adwords from Magento BI

1. Visit your Google [account settings](https://www.google.com/accounts/) page.
1. Under the Security section, and click the \'edit\' link next to Authorizing applications and sites.
1. Click the \'revoke access\' link next to Magento BI.

## Related

* [Reauthenticating integrations](https://support.magento.com/hc/en-us/articles/360016733151)
* [Track order referral source via Google ECommerce]({% link data-analyst/importing-data/integrations/google-ecommerce.md %})
* [Track user referral source in your database]({% link data-analyst/analysis/google-track-user-acq.md %})
* [Track user device, browser and OS data in your database](https://support.magento.com/hc/en-us/articles/360016732911)
* [Discover your most valuable acquisition sources and channels]({% link data-analyst/analysis/most-value-source-channel.md %})
* [Increase ROI on your advertising campaigns]({% link data-analyst/analysis/roi-ad-camp.md %})
* [How does Google Analytics UTM attribution work?]({% link data-analyst/analysis/utm-attributes.md %})

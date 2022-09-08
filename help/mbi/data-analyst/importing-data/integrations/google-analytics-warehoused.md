---
title: Connecting Google Analytics Warehoused
zendesk_id: 360016503212
---

{:.bs-callout-info}
[Requires Admin permissions](../administrator/user-management/user-management.md)

Google Analytics (GA) is the most widely-used web analytics service on the internet. Implementing GA on your website allows you to track how visitors use your site, what content is attractive, where visitors exit, and more. Google Analytics Warehoused is a separate integration from our existing GA integration. It will allow for better analysis due to having the Google Analytics data in your Data Warehouse, which is different than the live feed of the existing GA integration. Analyzing these metrics in MBI, alongisde other pieces of data, will improve your site\'s overall health and usability.

## Difference between GA Warehoused and Live Integration

The main differentiator is that one integration is stored (GA Warehoused), and the other is not (GA Live). In the case of GA Warehoused, this allows for manipulation of your GA data and gives you the ability to combine GA and other data sources to create insightful reporting.

Let\'s look at GA ad campaigns for an example of what can be done from a manipulation standpoint. Suppose you had multiple ad campaigns for Q4 with different names. The campaigns were a result of a specific marketing initiative. With warehoused data, we can create a new column that finds the campaign names in question and returns the Q4 initiative name of \"Operation Dumbo\".

The combination aspect allows GA data to be joined to other data in order to conduct analyses. For example, take \"Total Time On Site By Ad Campaign\" data from GA and join it up against \"Total Spent Per Campaign\" data from Facebook Ads to get a complete picture of how much engagement is costing you.

With the GA Live integration on the other hand, every GA chart is like a little silo that is not stored in your MBI data warehouse.

## Connecting Google Analytics Warehoused

{: .bs-callout-info}
Google Analytics Warehoused is a Premium Integration. Please contact Support if you have an interest in adding this integration to your subscription.

1. Go to the Connections page under **Admin > Integrations**.
1. Click the Add a Add Integration button, located on the right side of the screen.
1. Click the Google Analytics Warehoused icon. This will open the Google Analytics credentials page.
1. Enter your GA credentials. Upon completion of the authorization process, you will be redirected back to MBI.
1. A list of profile IDs will display. Check the profiles you want to connect to MBI. If you have multiple profiles and need some help identifying which is which, refer to the Connecting Multiple GA profiles section below.

## Connecting multiple Google Analytics profiles

You may have multiple websites connected to a single Google Analytics account, identified by their own GA profile ID. In this case, you will have the option of including all your profile IDs in MBI. Just check the profile IDs you\'d like to include during the profile selection step.

To identify a particular website\'s Google Analytics Profile ID:

1. Log into Google Analytics
1. Go to the particular website\'s GA dashboard
1. Look at the URL - the Profile ID corresponds to the 8 numbers following \"p\" at the end of the line: e.g., www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/

## Disconnecting Google Analytics Warehoused from MBI {#disconnect}

1. Visit your Google [account settings](https://www.google.com/accounts/) page.
1. Under the Security section,  and click the \'edit\' link next to Authorizing applications and sites.
1. Click the \'revoke access\' link next to MBI.

## Related documentation

* [Reauthenticating integrations](https://support.magento.com/hc/en-us/articles/360016733151)
* [Connecting Google Adwords](../data-analyst/importing-data/integrations/google-adwords.md)
* [Analyzing website activity and customer conversion rates](../data-analyst/analysis/web-act-cust-conversion.md)
* [Track user acquisition data using GA cookies](../data-analyst/analysis/google-track-user-acq.md)
* [Track user device and browser data using GA cookies](https://support.magento.com/hc/en-us/articles/360016732911)


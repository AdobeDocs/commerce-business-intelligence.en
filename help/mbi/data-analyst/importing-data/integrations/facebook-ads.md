---
title: Connecting Facebook Ads
zendesk_id: 360016505452
---

{:.bs-callout-info}
[Requires Admin permissions](../../../administrator/user-management/user-management.md)

![](../../../assets/Facebook_Logo.png)

You did your research, you created your ads, you launched your campaign on Facebook. Now it is time to analyze your ad spend data and see if your money is being spent effectively. Using your ad spend data, you can [measure campaign ROI by marrying your advertising cost and the customer lifetime value (CLV)](../data-analyst/analysis/roi-ad-camp.md) of users acquired from your campaigns.

Connecting your Facebook ad data to MBI is a simple three-step process:

1. [Add Facebook as a data source in MBI](../#stepone)
1. [Allow MBI access to your Facebook Ads data](../#steptwo)
1. [Select Facebook Ad Accounts for pulling data](../#stepthree)

## Add Facebook as a data source in MBI {#stepone}

1. To add the Facebook integration to your account, navigate to the Connections page under **Manage Data > Integrations**.
1. Click the **Add Integration** button, located on the right side of the screen above the Data Sources table.
1. Click the Facebook icon. This will display the Facebook authorization page.
1. Click the Authorize button.

## Allow MBI access to your Facebook Ads data {#steptwo}

After clicking the Authorize button, a small pop-up window will display:

 ![](../../../assets/Facebook_Access_Popup.png)

You will be taken through a series of steps to allow MBI to access data from your Public Profile, Facebook ads and related stats. "Okay" these steps to continue.

## Select Facebook Ads Accounts for pulling data {#stepthree}

1. After authentication is completed, you will be prompted to select the Facebook Ad Accounts you want to pull data from. Select the desired accounts by clicking the checkbox iin the Connect column.

     ![](../../../assets/Facebook_Ad_Accounts.png)

1. Click **Save Connections**.

   If the connection is successful, a *Connection Successful!* message will display at the top of the page.

## what is next? {#next}

Make sure that you are tracking Facebook campaigns in Google Analytics as per this [tutorial](https://www.facebook.com/business/google-analytics). This will ensure that the utm\_campaign field in Google Analytics is properly populated for your Facebook campaigns.

## Related

* [Reauthenticating integrations](https://support.magento.com/hc/en-us/articles/360016733151)
* [Connect your Google AdWords account](../integrations/google-ecommerce.md)
* [Track order referral source via Google eCommerce](../integrations/google-ecommerce.md)
* [Track user referral source in your database](../../analysis/google-track-user-acq.md)
* [Track user device, browser and OS data in your database](../../analysis/track-usr-dev-browser.md)
* [Discover your most valuable acquisition sources and channels](../../analysis/most-value-source-channel.md)
* [Increase ROI on your advertising campaigns](../../analysis/roi-ad-camp.md)
* [How does Google Analytics UTM attribution work?](../../analysis/utm-attributes.md)

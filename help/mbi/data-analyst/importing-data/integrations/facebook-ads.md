---
title: Connect Facebook Ads
description: Learn to analyze your ad spend data and see if your money is being spent effectively.
exl-id: 219a868b-f17c-4299-9e29-94db9156c9b6
---
# Connect [!DNL Facebook Ads]

>[!NOTE]
>
>Requires [Admin permissions](../../../administrator/user-management/user-management.md).

![](../../../assets/facebook-ads-logo.png)

You did your research, you created your ads, you launched your campaign on [!DNL Facebook]. Now it is time to analyze your ad spend data and see if your money is being spent effectively. Using your ad spend data, you can [measure campaign ROI by marrying your advertising cost and the customer lifetime value (CLV)](../../../data-analyst/analysis/roi-ad-camp.md) of users acquired from your campaigns.

Connecting your [!DNL Facebook Ad] data to [!DNL Commerce Intelligence] is a simple three-step process:

1. [Add [!DNL Facebook] as a data source in [!DNL Commerce Intelligence]](#stepone)
1. [Allow [!DNL Commerce Intelligence] access to your [!DNL Facebook Ads] data](#steptwo)
1. [Select [!DNL Facebook Ads] Accounts for pulling data](#stepthree)

## Add [!DNL Facebook] as a data source in [!DNL Commerce Intelligence] {#stepone}

1. To add the [!DNL Facebook] integration to your [!DNL Commerce Intelligence]account, navigate to the `Connections` page under **[!UICONTROL Manage Data** > **Integrations]**.
1. Click **[!UICONTROL Add Integration]**, located on the right.
1. Click the [!DNL Facebook] icon. This displays the [!DNL Facebook] authorization page.
1. Click **[!UICONTROL Authorize]**.

## Allow [!DNL Commerce Intelligence] access to your [!DNL Facebook Ads] data {#steptwo}

After clicking **[!DNL Facebook Authorize]**, a small pop-up window will display:

 ![](../../../assets/Facebook_Access_Popup.png)

You follow a series of steps to allow [!DNL Commerce Intelligence] to access data from your Public Profile, [!DNL Facebook Ads] and, related stats. Click **[!UICONTROL OK]** on these steps to continue.

## Select [!DNL Facebook Ads] Accounts for pulling data {#stepthree}

1. After authentication is completed, you will be prompted to select the [!DNL Facebook Ads] Accounts you want to pull data from. Select the desired accounts by clicking the checkbox in the `Connect` column.

     ![](../../../assets/Facebook_Ad_Accounts.png)

1. Click **[!UICONTROL Save Connections]**.

   If the connection is successful, a *Connection Successful!* message displays at the top of the page.

## What is next? {#next}

Make sure that you are tracking [!DNL Facebook] campaigns in [!DNL Google Analytics]. This ensures that the `utm\_campaign` field in [!DNL Google Analytics] is properly populated for your [!DNL Facebook] campaigns. 

## Related

* [Reauthenticating integrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
* [Connect your [!DNL Google Adwords] account](../integrations/google-ecommerce.md)
* [Track order referral source via [!DNL Google eCommerce]](../integrations/google-ecommerce.md)
* [Track user referral source in your database](../../analysis/google-track-user-acq.md)
* [Track user device, browser, and OS data in your database](../../analysis/track-usr-dev-browser.md)
* [Discover your most valuable acquisition sources and channels](../../analysis/most-value-source-channel.md)
* [Increase ROI on your advertising campaigns](../../analysis/roi-ad-camp.md)
* [How does [!DNL Google Analytics] UTM attribution work?](../../analysis/utm-attributes.md)

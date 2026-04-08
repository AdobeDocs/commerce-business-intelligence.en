---
title: Connect Facebook Ads
description: Learn to analyze your ad spend data and see if your money is being spent effectively.
exl-id: 219a868b-f17c-4299-9e29-94db9156c9b6
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/6TR559YyeTHT3KWl3oA4Bdnpr-HCowTXTTkvmP0I0tg
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
    internal-label: Accounts
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
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
---
# Connect [!DNL Facebook Ads]

>[!NOTE]
>
>Requires [Admin permissions](../../../administrator/user-management/user-management.md).

![Facebook Ads logo](../../../assets/facebook-ads-logo.png)

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

 ![Facebook access permission dialog for Commerce Intelligence](../../../assets/Facebook_Access_Popup.png)

You follow a series of steps to allow [!DNL Commerce Intelligence] to access data from your Public Profile, [!DNL Facebook Ads] and, related stats. Click **[!UICONTROL OK]** on these steps to continue.

## Select [!DNL Facebook Ads] Accounts for pulling data {#stepthree}

1. After authentication is completed, you will be prompted to select the [!DNL Facebook Ads] Accounts you want to pull data from. Select the desired accounts by clicking the checkbox in the `Connect` column.

     ![Facebook Ad Accounts selection interface](../../../assets/Facebook_Ad_Accounts.png)

1. Click **[!UICONTROL Save Connections]**.

   If the connection is successful, a *Connection Successful!* message displays at the top of the page.

## What is next? {#next}

Make sure that you are tracking [!DNL Facebook] campaigns in [!DNL Google Analytics]. This ensures that the `utm\_campaign` field in [!DNL Google Analytics] is properly populated for your [!DNL Facebook] campaigns. 

## Related

* [Reauthenticating integrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [Connect your [!DNL Google Adwords] account](../integrations/google-ecommerce.md)
* [Track order referral source via [!DNL Google eCommerce]](../integrations/google-ecommerce.md)
* [Track user referral source in your database](../../analysis/google-track-user-acq.md)
* [Track user device, browser, and OS data in your database](../../analysis/track-usr-dev-browser.md)
* [Discover your most valuable acquisition sources and channels](../../analysis/most-value-source-channel.md)
* [Increase ROI on your advertising campaigns](../../analysis/roi-ad-camp.md)
* [How does [!DNL Google Analytics] UTM attribution work?](../../analysis/utm-attributes.md)

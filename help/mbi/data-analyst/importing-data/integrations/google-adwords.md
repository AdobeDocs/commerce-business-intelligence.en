---
title: Connect Google Adwords
description: Learn to measure campaign ROI by marrying your advertising cost and the customer lifetime value (CLV) of users acquired from your campaigns.
exl-id: db99f817-2a2e-4194-9dd2-ec2d6b27a118
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/mZ8R2vPyFy8pGpYi4KhqocVnP-OlgMPGU3KJ4C9vsTo
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
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
---
# Connect [!DNL Google Adwords]

>[!NOTE]
>
>Requires [Admin permissions](../../../administrator/user-management/user-management.md).

![Google AdWords logo](../../../assets/Google_Adwords_logo.png)

You did your research, you created your ads, you launched your [!DNL Google] campaign. Now it is time to analyze your ad spend data and see if your money is being spent effectively. Using your ad spend data, you can [measure campaign ROI by marrying your advertising cost and the customer lifetime value (CLV)](../../analysis/roi-ad-camp.md) of users acquired from your campaigns.

Get started by entering your [!DNL Google Adwords] credentials into [!DNL Commerce Intelligence].

1. Go to the `Connections` page under **Manage Data > Integrations**.
1. Click **Add Integration**, located on the upper-right side of the screen.
1. Click the **[!DNL Google Adwords]** icon. This opens the [!DNL Google Adwords] credentials page.
1. Enter your [!DNL Google Analytics] credentials. Upon completion of the authorization process, you are redirected back to [!DNL Commerce Intelligence].
1. A list of profile IDs display. Check the profiles that you want to connect to [!DNL Commerce Intelligence].

     ![Google AdWords connection dialog showing profile selection](../../../assets/cnnct-profile.png)

1. Changes are saved automatically, so click **[!UICONTROL Back to Connections]** when you are done.

If you have multiple profiles and need some help identifying which is which, refer to the `Connecting Multiple Google Analytics profiles` section below.

## Connecting multiple [!DNL Google Analytics] profiles

You may have multiple websites connected to a single [!DNL Google Analytics] account, identified by their own [!DNL Google Analytics] Profile ID. In this case, you have the option of including all your Profile IDs in [!DNL Commerce Intelligence]. Check the profile IDs you want to include during the profile selection step.

**To identify a particular website's Google Analytics Profile ID:**

1. Log into [!DNL Google Analytics]
1. Go to the particular website's [!DNL Google Analytics] dashboard
1. Look at the URL - the Profile ID corresponds to the eight numbers following `p` at the end of the line:

     `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**`

## Disconnecting [!DNL Google Adwords]

1. Visit your [!DNL Google] [account settings](https://www.google.com/account/about/?hl=en) page.
1. Under the `Security` section, click **[!UICONTROL edit]** next to `Authorizing` applications and sites.
1. Click **[!UICONTROL revoke access]**.

## Related

* [Reauthenticating integrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [Track order referral source via [!DNL Google ECommerce]](../integrations/google-ecommerce.md)
* [Track user referral source in your database](../../analysis/google-track-user-acq.md)
* [Discover your most valuable acquisition sources and channels](../../analysis/most-value-source-channel.md)
* [Increase ROI on your advertising campaigns](../../analysis/roi-ad-camp.md)
* [How does [!DNL Google Analytics] UTM attribution work?](../../analysis/utm-attributes.md)

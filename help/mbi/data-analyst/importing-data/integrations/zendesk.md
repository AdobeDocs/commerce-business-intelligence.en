---
title: Connect Zendesk
description: Learn how to consolidate your help desk reporting in [!DNL MBI].
---
# Connect [!DNL Zendesk]

>[!NOTE]
>
>Requires [Admin permissions](../../../administrator/user-management/user-management.md).

![](../../../assets/Zendesk_logo.png)

Connecting your [!DNL Zendesk] data allows you to consolidate your help desk reporting in [!DNL MBI]. This allows you to optimize customer support and monitor help desk performance alongside your revenue.

Connecting your [!DNL Zendesk] data is a simple three-step process:

1. [Open the [!DNL Zendesk] credentials page in [!DNL MBI]](#stepone)
1. [Retrieve your [!DNL Zendesk] API Token](#steptwo)
1. [Enter your [!DNL Zendesk] login info and Token in [!DNL MBI]](#stepthree)

To complete this process, you will need to open two browser windows or tabs - one for [!DNL MBI], the other for your [!DNL Zendesk] account.

## Open the [!DNL Zendesk] credentials page in [!DNL MBI] {#stepone}

1. Go to the `Integrations` page under **[!UICONTROL Manage Data** > **Data Sources** > **Integrations]**.
1. Click **[!UICONTROL Add Integration]**, located on the right side of the screen.
1. Click the [!DNL Zendesk] icon. This will open the [!DNL Zendesk] credentials page.

## Retrieve your [!DNL Zendesk] API token {#steptwo}

1. In the window/tab where you are logged into your [!DNL Zendesk] account, click the Settings (gear) icon in the bottom-left corner of the screen.
1. When the `Settings` menu displays, locate the `Channels` section. Click **[!UICONTROL API]** in this section.
1. In the `Token Access` section of this page, click the checkbox next to `Enabled`. A list of Active API Tokens will display.
1. Click **[!UICONTROL Add New Token]**.
1. When prompted, enter a label for the token. We recommend using `MBI`, so you will know, at a glance, what application is using the token.
1. Click **[!UICONTROL Create]**.
1. An API token will be created. Copy this token; it will be used in the next step.

## Enter [!DNL Zendesk] login info and API token into [!DNL MBI] {#stepthree}

1. Enter your [!DNL Zendesk] site prefix and login email in the [!DNL Zendesk] credentials page in [!DNL MBI].
1. Enter your API token.
1. Click **[!UICONTROL Save & Connect]**. If the connection is successful, a *Connection Successful!* message will display at the top of the screen.

## Related:

* [Expected [!DNL Zendesk] data](../integrations/exp-zendesk-data.md)
* [Reauthenticating integrations](https://support.magento.com/hc/en-us/articles/360016733151)
---
title: Connect Zendesk
description: Learn how to consolidate your help desk reporting in [!DNL Commerce Intelligence].
exl-id: 1c7f7c5c-4b1c-4bcf-8f1d-2b4cf9cdb0fb
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/KBUuqTDD9s3qXDktcV3RzLx4zxtAFwAkKPbsQE2YGtI
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
  - id: f42e0a1a-0d79-488d-a83f-f2c30672b137
    internal-label: Reporting
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
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
    internal-label: Reporting
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
---
# Connect [!DNL Zendesk]

>[!NOTE]
>
>Requires [Admin permissions](../../../administrator/user-management/user-management.md).

![Zendesk logo](../../../assets/Zendesk_logo.png)

Connecting your [!DNL Zendesk] data allows you to consolidate your help desk reporting in [!DNL Commerce Intelligence]. This allows you to optimize customer support and monitor help desk performance alongside your revenue.

Connecting your [!DNL Zendesk] data is a simple three-step process:

1. [Open the [!DNL Zendesk] credentials page in [!DNL Commerce Intelligence]](#stepone)
1. [Retrieve your [!DNL Zendesk] API Token](#steptwo)
1. [Enter your [!DNL Zendesk] login info and Token in [!DNL Commerce Intelligence]](#stepthree)

To complete this process, you need to open two browser windows or tabs - one for [!DNL Commerce Intelligence], the other for your [!DNL Zendesk] account.

## Open the [!DNL Zendesk] credentials page in [!DNL Commerce Intelligence] {#stepone}

1. Go to the `Integrations` page under **[!UICONTROL Manage Data** > **Data Sources** > **Integrations]**.
1. Click **[!UICONTROL Add Integration]**, located on the right side of the screen.
1. Click the [!DNL Zendesk] icon. This opens the [!DNL Zendesk] credentials page.

## Retrieve your [!DNL Zendesk] API token {#steptwo}

1. In the window/tab where you are logged into your [!DNL Zendesk] account, click the Settings (gear) icon in the bottom-left corner of the screen.
1. When the `Settings` menu displays, locate the `Channels` section. Click **[!UICONTROL API]** in this section.
1. In the `Token Access` section of this page, click the checkbox next to `Enabled`. A list of Active API Tokens display.
1. Click **[!UICONTROL Add New Token]**.
1. When prompted, enter a label for the token. Adobe recommends using `Commerce Intelligence`, so you know, at a glance, what application is using the token.
1. Click **[!UICONTROL Create]**.
1. An API token is created. Copy this token; it will be used in the next step.

## Enter [!DNL Zendesk] login info and API token into [!DNL Commerce Intelligence] {#stepthree}

1. Enter your [!DNL Zendesk] site prefix and login email in the [!DNL Zendesk] credentials page in [!DNL Commerce Intelligence].
1. Enter your API token.
1. Click **[!UICONTROL Save & Connect]**. If the connection is successful, a *Connection Successful!* message displays at the top of the screen.

## Related:

* [Expected [!DNL Zendesk] data](../integrations/exp-zendesk-data.md)
* [Reauthenticating integrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)

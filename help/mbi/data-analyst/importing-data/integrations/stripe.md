---
title: Connect Stripe
description: Learn how to manage and track your business's payment and invoice data.
exl-id: c038f2a9-b2bd-4e45-93f9-12d2e5077b31
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/S6-otAlCeS8aKQ6K-xZH2ZaqEjZ-ZZ6fMWXtFFafu6c
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
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
# Connect [!DNL Stripe]

>[!NOTE]
>
>Requires [Admin permissions](../../../administrator/user-management/user-management.md).

![Stripe logo](../../../assets/stripe-logo.png)

[!DNL Stripe] allows you to manage and track your business's payment and invoice data. Connecting your [!DNL Stripe] account to [!DNL Commerce Intelligence] is a simple two-step process:

1. [Add [!DNL Stripe] as a data source in [!DNL Commerce Intelligence]](#stepone)
1. [Allow [!DNL Commerce Intelligence] access to your [!DNL Stripe] Data](#steptwo)

## Add [!DNL Stripe] as a data source {#stepone}

1. Go to the `Connections` page under **[!UICONTROL Admin** > **Connections]**.
1. Click **[!UICONTROL Add a Data Source]**, located on the right side of the screen above the `Data Sources` table.
1. Click the [!DNL Stripe] icon. This displays the `[!DNL Stripe] authorization` page.
1. Click **[!UICONTROL Connect with Stripe]**.

## Allow [!DNL Commerce Intelligence] access to your [!DNL Stripe] data {#steptwo}

After clicking **[!UICONTROL Connect with Stripe]**, an access request page appears.

1. Click **[!UICONTROL Sign in with Stripe to Continue]**.

1. Enter your credentials and click **[!UICONTROL Sign in to your account]**.

1. Your credentials will be validated and you will be directed back to [!DNL Commerce Intelligence].

1. If the connection is successful, a *Connection Successful!* message appears at the top of the screen.

## Related:

The [[!DNL Stripe] API Documentation](https://stripe.com/docs/api) can be a useful resource for learning more about how [!DNL Stripe] is integrated with [!DNL Commerce Intelligence].

* [Expected [!DNL Stripe] data](../integrations/stripe-data.md)
* [Reauthenticating integrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)

---
title: Connect Adobe Analytics
description: Learn to bring together the end-to-end customer journey focus of [!DNL Adobe Analytics] and the eCommerce focus you rely on from [!DNL Commerce Intelligence].
exl-id: 824e1ee4-6b88-42f7-b265-29330dbc4407
---
# Connect [!DNL Adobe Analytics]

>[!NOTE]
>
>Requires [Admin permissions](../../../administrator/user-management/user-management.md).

![](../../../assets/adobe-analytic-slogo.png)

The [!DNL Adobe Analytics] integration for [!DNL Adobe Commerce Intelligence] enables you to bring together the end-to-end customer journey focus of [!DNL Adobe Analytics] and the eCommerce focus you rely on from [!DNL Commerce Intelligence]. This gives you a complete picture of your store's overall performance.

More specifically, the [!DNL Adobe Analytics] integration for [!DNL Commerce Intelligence] provides functionality for merchants to start combining their [!DNL Adobe Commerce] and [!DNL Adobe Analytics] data sets.

- Create a connection from your existing [!DNL Adobe Analytics] account into [!DNL Commerce Intelligence].

- Select up to 25 metrics and dimensions from one report suite to replicate into your Data Warehouse.

- Use all standard [!DNL Commerce Intelligence] functionality to transform, join, and report on replicated [!DNL Adobe Analytics] data.

## Connection Prerequisites

The following information is needed to connect:

- [!DNL Adobe Analytics] login credentials

- `Name` and/or `ID` of [!DNL Adobe Analytics] report suite to replicate data from

- List of metrics and dimensions to replicate into [!DNL Commerce Intelligence]

## Connecting the [!DNL Adobe Analytics] Integration for [!DNL Commerce Intelligence]

1. Go to the `Integrations` page under **[!DNL Manage Data** > **Integrations]**.

1. Click **[!UICONTROL Add an Integration]**.

1. Click the **[!UICONTROL Adobe Analytics]** icon to access the page that allows you to authorize your [!DNL Adobe Analytics] account connection.

1. Click **[!UICONTROL Authorize with Adobe Analytics]**.

1. Enter your [!DNL Adobe Analytics] credentials. After successful authorization, you are redirected back to [!DNL Commerce Intelligence].

1. A list of available report suites displays. Select the report suite from which you want to import the data, then click **[!UICONTROL Continue]**.

1. The metrics and dimensions selection screen displays. Select at least one metric and at least one dimension, up to a combined total of 25 metrics and dimensions. Search by name or scroll to find your components, then click the checkboxes to select. Click **[!UICONTROL Continue]**.

1. The selected report suite displays in a table. Click **[!UICONTROL Save]** to confirm your selection.

1. Inform the [!DNL Commerce Intelligence] [Support team](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) that your integration is authorized, and they run the initial connection process for you.

After the initial connection process runs, your table will be available in the Data Warehouse page, under the `All Tables` tab. Select the columns that you wish to replicate, and the data will appear after the next full update.

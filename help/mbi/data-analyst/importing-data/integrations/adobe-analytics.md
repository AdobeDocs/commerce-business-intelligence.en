---
title: Connect Adobe Analytics
description: Learn to bring together the end-to-end customer journey focus of [!DNL Adobe Analytics] and the eCommerce focus you rely on from [!DNL MBI].
---

# Connect [!DNL Adobe Analytics]

>[!NOTE]
>
>Requires [Admin permissions](../../../administrator/user-management/user-management.md).

The [!DNL Adobe Analytics] integration for [!DNL MBI] enables you to bring together the end-to-end customer journey focus of [!DNL Adobe Analytics] and the eCommerce focus you rely on from [!DNL MBI], to get a more complete picture of your store's overall performance.

More specifically, the [!DNL Adobe Analytics] integration for [!DNL MBI] provides functionality for merchants to start combining their Commerce and Analytics data sets.
- Create a connection from your existing [!DNL Adobe Analytics] account into [!DNL MBI].
- Select up to 25 metrics and dimensions from 1 report suite to replicate into your [!DNL MBI] data warehouse.
- Use all standard [!DNL MBI] functionality to transform, join, and report on replicated [!DNL Adobe Analytics] data.

## Connection Prerequisites

The following information is needed to connect:
- [!DNL Adobe Analytics] login credentials
- `Name` and/or `ID` of [!DNL Adobe Analytics] report suite to replicate data from
- List of metrics and dimensions to replicate into [!DNL MBI]

## Connecting the [!DNL Adobe Analytics] Integration for MBI

1. Go to the `Integrations` page under **[!DNL Manage Data** > **Integrations]**.
1. Click **[!UICONTROL Add an Integration]**, located on the right side of the screen.
1. Click the **[!UICONTROL Adobe Analytics]** icon to access the page that allows you to authorize your [!DNL Adobe Analytics] account connection.
1. Click **[!UICONTROL Authorize with Adobe Analytics]**.
1. Enter your [!DNL Adobe Analytics] credentials. After successful authorization, you are redirected back to [!DNL MBI].
1. A list of available report suites displays. Select the report suite from which you want to import the data, then click **[!UICONTROL Continue]**.
1. The metrics and dimensions selection screen displays. Select at least one metric and at least one dimension, up to a combined total of 25 metrics and dimensions. Search by name or scroll to find your components, then click the checkboxes to select. Click **[!UICONTROL Continue]**.
1. The selected report suite displays in a table. Click **[!UICONTROL Save]** to confirm your selection.
1. Inform the [!DNL MBI] Support team that your integration is authorized, and they will run the initial connection process for you.

After the initial connection process runs, your table will be available in the Data Warehouse page, under the `All Tables` tab. Select the columns you wish to replicate, and the data will appear after the next full update.

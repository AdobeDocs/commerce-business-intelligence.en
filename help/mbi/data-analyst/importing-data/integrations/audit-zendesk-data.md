---
title: Audit Zendesk data
description: Learn the steps for exporting your Zendesk data.
exl-id: 3c8dcc72-3623-4c4e-a941-f431a97571e0
---
# Audit Zendesk data

Found something strange in your [[!DNL Zendesk] data](../integrations/exp-zendesk-data.md)? To pinpoint the issue, we need to explore your data. This can be done by exporting your [!DNL Zendesk] data to a downloadable file.

## Enabling data export

Data export is not currently enabled for all [!DNL Zendesk] accounts. To activate this feature, [submit a support ticket](../../../guide-overview.md), mentioning your [!DNL Zendesk] subdomain name. 

>[!NOTE] 
>
>Only `Enterprise` and `Plus` plans currently have access to this feature.

After data export is enabled, only administrators in a specific email domain can export data from your [!DNL Zendesk] account. This email domain is typically the same email domain as your [!DNL Zendesk]. The account owner's email domain is used as the default, but you can change the domain if necessary.

## Exporting to a downloadable file

1. Click the Admin icon (gear logo) in the sidebar and choose **[!UICONTROL Manage** > **Reports]**.
1. Click the **[!UICONTROL Export]** tab.
1. Click **[!UICONTROL Request file]** beside Full XML Export as seen in the image below.

   At this point, a build will begin; you will be notified via email when it completes.
   ![reports_export_new.png](../../../assets/reports_export_new.png)

1. Click the link in your email notification to download a zip file containing the report.

   This download link is valid for at least three days.

This process builds an XML file containing all information stored in your current [!DNL Zendesk] account, including ticket data (with comments), user data, and account data. At this point, you can [submit a support ticket](../../../guide-overview.md) (be sure to attach this file!) so we can take a closer look at your data. If the file is too large, share it with the [!DNL MBI] team via [!DNL Dropbox] or [!DNL Google Drive].

For more information about [!DNL Zendesk] file exports, refer to the official [[!DNL Zendesk] export documentation](https://support.zendesk.com/entries/23002207-Exporting-data-to-a-CSV-or-XML-file-Plus-and-Enterprise-).

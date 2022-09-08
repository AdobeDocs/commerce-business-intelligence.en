---
title: Auditing Zendesk data
zendesk_id: 360016506272
---

Found something strange in your [Zendesk data](../data-analyst/importing-data/integrations/exp-zendesk-data.md)? To pinpoint the issue, we need to explore your data. This can be done by exporting your Zendesk data to a downloadable file.

## Enabling data export

Data export is not currently enabled for all Zendesk accounts. To activate this feature, [submit a support ticket](../getting-started/support.md), mentioning your Zendesk subdomain name. **Keep in mind that only Enterprise and Plus plans currently have access to this feature**.

After data export is enabled, only administrators in a specific email domain can export data from your Zendesk account. This email domain is typically the same email domain as your Zendesk. The account owner’s email domain is used as the default, but you can change the domain if necessary.

## Exporting to a downloadable file

1. Click the Admin icon (gear logo) in the sidebar and choose **Manage > Reports**.
1. Click the **Export** tab.
1. Click **Request file** beside Full XML Export as seen in the image below.

   At this point, a build will begin; you will be notified via email when it completes.
   ![reports_export_new.png](../assets/reports_export_new.png)
1. Click the link in your email notification to download a zip file containing the report.

   This download link is valid for at least three days.

This process builds an XML file containing all information stored in your current Zendesk account, including ticket data (with comments), user data, and account data. At this point, you can [submit a support ticket](../getting-started/support.md) (be sure to attach this file!) so we can take a closer look at your data. If the file is too large, share it with the MBI team via Dropbox or Google Drive.

For more information about Zendesk file exports, refer to the official [Zendesk export documentation](https://support.zendesk.com/entries/23002207-Exporting-data-to-a-CSV-or-XML-file-Plus-and-Enterprise-).

---
title: Audit Zendesk data
description: Learn the steps for exporting your Zendesk data.
exl-id: 3c8dcc72-3623-4c4e-a941-f431a97571e0
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/EQmiSbzzvOONQ8-F1U9uMVpgXUKd2PEjcLXLVSgQSm8
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
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
---
# Audit Zendesk data

Found something strange in your [[!DNL Zendesk] data](../integrations/exp-zendesk-data.md)? To pinpoint the issue, you need to explore your data. This can be done by exporting your [!DNL Zendesk] data to a downloadable file.

## Enabling data export

Data export is not currently enabled for all [!DNL Zendesk] accounts. To activate this feature, [submit a support ticket](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html), mentioning your [!DNL Zendesk] subdomain name. 

>[!NOTE] 
>
>Only `Enterprise` and `Plus` plans currently have access to this feature.

After data export is enabled, only administrators in a specific email domain can export data from your [!DNL Zendesk] account. This email domain is typically the same email domain as your [!DNL Zendesk]. The account owner's email domain is used as the default, but you can change the domain if necessary.

## Exporting to a downloadable file

1. Click the Admin icon (gear logo) in the sidebar and choose **[!UICONTROL Manage** > **Reports]**.
1. Click the **[!UICONTROL Export]** tab.
1. Click **[!UICONTROL Request file]** beside Full XML Export as seen in the image below.

   At this point, a build begins; you are notified via email when it completes.
   ![reports_export_new.png](../../../assets/reports_export_new.png)

1. Click the link in your email notification to download a zip file containing the report.

   This download link is valid for at least three days.

This process builds an XML file containing all information stored in your current [!DNL Zendesk] account, including ticket data (with comments), user data, and account data. At this point, you can [submit a support ticket](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) (be sure to attach this file!) so you can take a closer look at your data. If the file is too large, share it with the [!DNL Commerce Intelligence] team via [!DNL Dropbox] or [!DNL Google Drive].

For more information about [!DNL Zendesk] file exports, refer to the official [[!DNL Zendesk] export documentation](https://support.zendesk.com/hc/en-us/articles/4408886165402-Exporting-data-to-a-JSON-CSV-or-XML-file).

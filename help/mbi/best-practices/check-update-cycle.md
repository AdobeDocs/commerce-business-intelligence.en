---
title: Checking the Update Cycle Status
description: Learn how to check the update cycle status.
exl-id: bd65f2bb-86c1-4e83-a132-797694ddb086
role: Admin, Data Architect, Data Engineer, User
feature: Dashboards
---
# Update cycle progress

When you log into your [!DNL Adobe Commerce Intelligence] dashboard, there are several ways to check the status of your last update cycle. It all depends on the type of [user permissions](../administrator/user-management/user-management.md) that you have.

## Why Should I Check the Update Cycle Status?

Checking the status update cycle is useful when you are auditing the data in your [!DNL Commerce Intelligence] account. If you see [results that do not meet your expectations](../data-analyst/data-warehouse-mgr/data-and-updates-faq.md), for example, daily sales in [!DNL Commerce Intelligence] are not matching what you are seeing in your e-commerce platform or in your [[!DNL Google] e-commerce revenue](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-google-ecommerce-revenue-discrepancies.html) you can check the last data point to see if the issue is resolved once an update completes.

## [!UICONTROL Read-Only] and [!UICONTROL Standard] Users

`Read-only` users can log into their dashboard and see how recently the data has been updated by hovering over the icon at the top right of the page. This shows when the last data point was pulled.

![Last successful data update timestamp shown in interface](../../mbi/assets/last-success-data.png)

## [!UICONTROL Admin] Users

`Admin` users can log into the dashboard and see the last data point above, along with a brief status icon of their account integrations.

For more detail, admin users can click **[!UICONTROL Manage Data]** > **[!UICONTROL Integrations]**.

![Manage Data integrations page showing connection details and update status](../../mbi/assets/detail-manage-data-integrations.png)

This page shows you the current update status and the time of the last completed update.

If an update is in progress, you see a link to request an email notification once the update completes.

If an update is not in progress, you see a link to force an update to start.

>[!NOTE]
>
>If you have blackout hours (time when you do not want [!DNL Commerce Intelligence] to update your data) set, forcing an update starts an update cycle that does not respect the limitations of those blackout hours.


## Check the update cycle status using the API

You can retrieve the most recent completed update cycle using the **Update Cycle Status API**.

**Request**

```bash
curl -sS -H "X-RJM-API-Key: <EXPORT-API-KEY>" \
  https://api.rjmetrics.com/0.1/client/<CLIENT_ID>/fullupdatestatus
```

**Response (example)**

```json
{
  "clientId": 194,
  "lastCompletedUpdateJob": {
    "id": 13554,
    "type": { "id": 2, "name": "Full Update" },
    "start": "2025-12-09 03:26:25",
    "end": "2025-12-09 03:29:03",
    "status": { "id": 4, "name": "Completed Successfully" }
  },
  "lastCompletedUpdateJobWithDataSync": null,
  "timezoneAbbreviation": "EST"
}
```

For parameters, authentication, errors, and rate limits, see [Update Cycle Status API](https://developer.adobe.com/commerce/services/reporting/update-cycle/) in the developer documentation. 

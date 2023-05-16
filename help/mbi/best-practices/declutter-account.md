---
title: Decluttering your [!DNL Commerce Intelligence] Account
description: Learn how to clean up your [!DNL Commerce Intelligence] account.
exl-id: 5fcdac2d-41ca-4011-b646-a699d9ecc6e4
---
# Clean up your [!DNL Adobe Commerce Intelligence] Account

Whether you have been with [!DNL Commerce Intelligence] for six months or six years, maintaining a tidy account is paramount to your organization getting the most out of the platform. Over time, it is natural for there to be users, dashboards, reports, metrics, and columns that are no longer needed. Perhaps you created a report for one-time use and forgot about it or a user who left your company never had their account deactivated.

With [standardized, clear naming for all elements](../best-practices/naming-elements.md)) of your [!DNL Commerce Intelligence] account, the account audit steps below help you reduce the clutter and unnecessary analyses for your users. One additional benefit includes [potentially faster update cycles](../best-practices/reduce-update-cycle-time.md).

## Step 1: Identify Your Non-Active Users

The first step in cleaning up your account is to deactivate the accounts of your non-active users, such as people who have left the company or no longer use [!DNL Commerce Intelligence] in their current roles.

To do this - click your company's name in the upper-right navigation bar, then select **[!UICONTROL Manage Users]**. Next, select the user you want to deactivate and click **[!UICONTROL Deactivate User]**. 

>[!NOTE]
>
>You need [Admin permissions](../administrator/user-management/user-management.md) to do this.

>[!WARNING]
>
>Deactivating a user removes the charts, dashboards, and other assets created by that user. If you want to preserve these assets, contact the [!DNL Commerce Intelligence] [support](../guide-overview.md#Submitting-a-Support-Ticket) team before deactivating the user. Support can help you transfer these assets to another user.

### Reactivate a User

To reactivate a user, reinvite the user by recreating their account with the same email address that was deactivated, and their access and the data they owned are restored at login.

## Step 2: Delete Unused Dashboards and Reports

The next step in auditing your account is to delete any unused dashboards and reports. 

>[!NOTE]
>
>You need `Admin` or `Standard` [user permissions](../administrator/user-management/user-management.md) to do this.

Every user with `Admin` or `Standard` access can create reports and dashboards. For that reason, everyone with these permissions must follow the steps below to identify and remove unused reports.

### Review Your Dashboards and Reports

Before you delete anything, you should review your reports and dashboards to assess what is in use. While you can use the **[!UICONTROL find unused reports]** feature described below, any initial review makes your cleanup efforts much more productive.

### Deleting Dashboards and Reports

After you access your dashboards and reports, you can then begin cleaning up your account.

**To Remove a Report from a Dashboard**

1. Locate the report that you want to remove on the dashboard.
1. Select **[!UICONTROL Options]** in the top-right corner of the report.
1. Click **[!UICONTROL Remove From Dashboard]**.

**To Delete an Entire Dashboard**

1. Select **[!UICONTROL Manage Data]**, then **[!UICONTROL Dashboards**].
1. Click on the dashboard that you want to delete.
1. Click **[!UICONTROL Delete Dashboard]**.

You can also select **[!UICONTROL Dashboard Options]**, then **[!UICONTROL Delete]** from the dashboard itself.

![](../../mbi/assets/Delete_from_dashboard.png)

>[!NOTE]
>
>Deleting a dashboard does not delete the reports within it, so you have to take one more step to delete the reports.

**To Delete Unused Reports**

1. Select **[!UICONTROL Manage Data]**, then **[!UICONTROL Reports]**.
1. Check the **Only show unused reports** box located beneath the metrics list. This creates a list of reports that are not used in a dashboard or email summary.
1. Select the reports that you want to delete. You can select all by clicking the checkbox above the report list.
1. Click **[!UICONTROL Delete Selected]**.

Here is a look at the unused report deletion process:

![](../../mbi/assets/unused_reports.png)

## Step 3: Delete Unused Metrics

After you have cleaned up your users list, dashboards, and reports, you can move onto auditing your list of metrics. This helps you identify anything that might be outdated - for example, a new metric was created with a different definition - or not in use.

1. To generate a list of dependent reports for a metric, go to **[!DNL Manage Data]**, then select Click **[!UICONTROL Metrics]**.
1. Click **[!UICONTROL Edit]** next to a metric.
1. At the bottom of the page, you see a section called **[!UICONTROL Dependent Charts]**. Click the link to generate a dependent reports list for this metric.
1. After the system completes the check, [!DNL Commerce Intelligence] displays a list of dashboards, reports, and users using this metric.

![](../../mbi/assets/report_dependecies.png)

If you decide that the metric is no longer needed, navigate back to the **[!UICONTROL Metrics]** page by clicking **[!UICONTROL Back to Metric List]** to find the metric you want to delete. Click **[!UICONTROL Delete]**.

## Step 4: Assess Your Synced Columns

The last step is to assess the columns currently being synced in your Data Warehouse. Not only can unsyncing columns declutter your account, it can also potentially reduce your update time.

If you would like to pursue this, reach out to [!DNL Commerce Intelligence] [Support](../guide-overview.md#Submitting-a-Support-Ticket). The Support team can create a report that includes all columns that are not being used in any dashboard for any user and that are not used in email summaries, excluding SQL Reports. You can then use this report as a guide for selecting columns to unsync via the Data Warehouse Manager.

>[!NOTE]
>
>You can always start syncing these columns again in the future. Unsyncing a column removes any data from your Data Warehouse; it only means that this column is not checked for new or updated values during the update cycle.

**To Unsync a Column (or Columns)**

1. Go to **[!DNL Manage Data]**, then **[!UICONTROL Data Warehouse]**.
1. In the **[!UICONTROL Synced Tables]** list, navigate to the table that contains the column.
1. Check one or more boxes next to one or more columns that you want to unsync. 
   >[!NOTE]
   >
   >You cannot unsync a Primary Key column without dropping the entire table.

1. Click **[!UICONTROL Remove]** to unsync one or more columns.

Here is a look at the whole process:

![](../../mbi/assets/drop_column.png)

## Wrapping up

That is it! Your [!DNL Commerce Intelligence] account should now be tidier and easier to navigate for you and your team.

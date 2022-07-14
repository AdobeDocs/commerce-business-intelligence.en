---
title: Decluttering your Magento BI Account
zendesk_id: 360016730171
---

Whether you’ve been with Magento BI for 6 months or 6 years, maintaining a tidy account is paramount to your organization getting the most out of the platform. Over time, it’s natural for there to be users, dashboards, reports, metrics, and columns that are no longer needed. Perhaps you created a report for one-time use and forgot about it, or a user who left your company never had his or her account deactivated.

In conjunction with [standardized, clear naming for all elements]({% link best-practices/naming-elements.md %})) of your Magento BI account, the account audit steps below will help you reduce the clutter and unnecessary analyses for your users. One additional benefit includes [potentially faster update cycles]({% link best-practices/reduce-update-cycle-time.md %}).

## Step 1: Identify Your Non-Active Users

The first step in cleaning up your account is to deactivate the accounts of your non-active users, such as people who have left the company or no longer use Magento BI in their current roles.

You can do this by clicking your company\'s name in the top-right corner of the top navigation bar, then selecting **Manage Users**. Next, select the user you want to deactivate, and click the **Deactivate User** button. Note that you need [Admin permissions]({% link administrator/user-management/user-management.md %}) to do this.

{:.bs-callout-warning}
Deactivating a user will also remove the charts, dashboards, and other assets created by that user. If you want to preserve these assets, reach out to the Magento BI [support]({% link getting-started/support.md %}) team before deactivating the user. Support can help you transfer these assets to another user.

### Reactivate a User

To reactivate a user, reinvite the user by recreating their account with the same email address that was deactivated, and their access and the data they owned will be restored upon login.

## Step 2: Delete Unused Dashboards and Reports

The next step in auditing your account is to delete any unused dashboards and reports. Note that you need [Admin or standard user permissions]({% link administrator/user-management/user-management.md %}) to do this.

Every user with Admin or Standard access can create reports and dashboards. For that reason, everyone with these permissions must follow the steps below to identify and remove unused reports.

### Review Your Dashboards and Reports

Before you delete anything, you should review your reports and dashboards to assess what’s currently in use. While you can use the **find unused reports** feature described below, any initial review will make your cleanup efforts much more productive.

### Deleting Dashboards and Reports

After you access your dashboards and reports, you can then begin cleaning up your account.

**To Remove a Report from a Dashboard**

1. Locate the report you want to remove on the dashboard.
1. Select the **Options** button in the top-right corner of the report.
1. Click **Remove From Dashboard**.

**To Delete an Entire Dashboard**

1. Select **Manage Data**, then **Dashboards**.
1. Click on the dashboard you want to delete.
1. Click **Delete Dashboard**.

You can also select **Dashboard Options**, then **Delete** from the dashboard itself.

![]({% link images/Delete_from_dashboard.png %})

Note that deleting a dashboard does not delete the reports within it, so you’ll have to take one more step to delete the reports.

**To Delete Unused Reports**

1. Select **Manage Data**, then **Reports**.
1. Check the **Only show unused reports** box located beneath the metrics list. This will create a list of reports that are not used in a dashboard or email summary.
1. Select the reports you want to delete. You can select all by clicking the checkbox above the report list.
1. Click the **Delete Selected** button.

Here’s a look at the unused report deletion process:

![]({% link images/unused_reports.png %})

## Step 3: Delete Unused Metrics

After you’ve cleaned up your users list, dashboards, and reports, you can move onto auditing your list of metrics. This will help you identify anything that might be outdated - for example, a new metric was created with a different definition - or not in use.

1. To generate a list of dependent reports for a metric, go to **Manage Data**, then select **Metrics**.
1. Click the **Edit** link next to a metric.
1. At the bottom of the page, you’ll see a section called **Dependent Charts**. Click the link to generate a dependent reports list for this metric.
1. After the system completes the check, Magento BI displays a list of dashboards, reports, and users utilizing this metric.

![]({% link images/report_dependecies.png %})

If you decide that the metric is no longer needed, navigate back to the **Metrics** page by clicking the **Back to Metric List** link at the top of the page and find the metric you want to delete. Click **Delete**.

## Step 4: Assess Your Synced Columns

The last step is to assess the columns currently being synced in your data warehouse. Not only can unsyncing columns declutter your account, it can also potentially reduce your update time.

If you would like to pursue this, reach out to Magento BI [support]({% link getting-started/support.md %}). The support team can create a report that includes all columns that are not being used in any dashboard for any user and that are not used in email summaries, excluding SQL Reports. You can then use this report as a guide for selecting columns to unsync via the Data Warehouse Manager.

Note that you can always start syncing these columns again in the future. Unsyncing a column won’t remove any data from your data warehouse; it only means this column won’t be checked for new or updated values during the update cycle.

**To Unsync a Column (or Columns)**

1. Go to **Manage Data**, then **Data Warehouse**.
1. In the **Synced Tables** list, navigate to the table that contains the column.
1. Check the box(es) next to the column(s) you want to unsync. **Note that you can’t unsync a Primary Key column** without dropping the entire table.
1. Click **Remove** to unsync the column(s).

Here’s a look at the whole process:

![]({% link images/drop_column.png %})

## Wrapping up

That’s it! Your Magento BI account should now be tidier and easier to navigate for you and your team. For more best practices including optimizing your update time and database, click [here]({% link best-practices.md %}).

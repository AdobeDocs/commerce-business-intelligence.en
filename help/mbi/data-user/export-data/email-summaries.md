---
title: Creating automated email summaries
zendesk_id: 360016730911
---

Email summaries are a powerful communication tool you can use to share the current status and trends of your business with key stakeholders. With email summaries you can:

* Email graphical summaries that include reports
* Include or exclude the email summary author from receiving the email
* Schedule when the email is sent
* Edit, delete, and pause existing scheduled email summaries

## Create New Email Summary

1. Select **Manage Data** then **Email Summary** in the sidebar.

   If this is the first time you are creating an email summary, this page does not display any saved summaries.

1. Click the **Create New Email Summary** button in the top right corner.

1. Enter a name for the summary.

   Choose a name that conveys what is included in the summary. For example, _AOV Comparison_.

1. In the **Choose Content** section, select the reports you want to include in the summary.

   You can select up to 10 reports that you own. After you select a report, use the icons that appear to select if you want that report sent as a table or a chart. If you saved the report as a number, you can only send it as a number. For information about sending an email summary that contains a report with stale data, see [Managing your account settings](../administrator/account-management/managing-account-settings.md).

  {: .bs-callout-info}
  **Note**: Cohort reports are only available if you are using the new architecture.

1. (Optional) Select **Send Email To Me** if you want to receive the email.

1. To include other users on the email, enter their email addresses in the **Add Email Recipients** field separated by commas, spaces, tabs, or semi-colons.

## Schedule Email Summary

In the **Set when to send the Email Summary** field, you can specify when to send the email summaries. Options are:

* **Manual**
* **Once**
* **Repeating**

### Save Email Summary to be Sent at a Later Date

1. Select **Manual** from the **Set when to send the Email Summary** field.

1. Click **Save**.

   This saves the summary to the list of email summaries.

1. When you are ready to send the summary, click the gear icon and select **Send Now**.

### Send Email Summary Once

1. Select **Once** from the **Set when to send the Email Summary** field.

1. Specify the start date in the **Select Start Date** calendar.

1. Specify the time to send the email in the **Select time to send** field.

### Create Repeating Schedule

1. Select **Repeating** from the **Set when to send the Email Summary** field.

1. In the **Set Frequency** field, select `Daily`, `Weekly`, or `Monthly`.

1. Specify the start date in the **Select Start Date** calendar.

1. Specify the time to send the email in the **Select time to send** field.

1. (Optional) To specify an end date, select **End Date** and select the end date from the calendar.

## Modify Existing Email Summary

After you create and save an email summary, the **Email Summaries** page displays a list of all saved summaries. You can expand (`+`) each row for more information. The columns in this view are:

* **Email Name** - Name of the email summary
* **Content** - Type of content within the summary, such as the names of any reports. For information about sending an email summary that contains a report with stale data, see [Managing your account settings](../administrator/account-management/managing-account-settings.md).
* **Scheduled** - Frequency, date, and time the email summary is sent
* **Recipients** - Recipients of email summary
* **Created Date** - Date the email summary was created
* **Status** - `Paused` or `Active`

Click the gear icon to the right of each row to:

* **Send Now** - Sends the email summary immediately to all specified recipients
* **Edit** - Allows you to modify the details of the email summary
* **Pause/Active** - Allows you to pause the email summary from being delivered or enable the summary based on how it is configured
* **Delete** - Deletes the email summary

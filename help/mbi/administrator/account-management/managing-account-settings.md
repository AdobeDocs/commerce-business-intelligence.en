---
title: Manage your account settings
description: Learn how to customize a number of account settings for your data warehouse.
---
# Customizing your account settings

>[!NOTE]
>
>[Requires Admin permissions.](../../administrator/user-management/user-management.md)

In your[!DNL MBI]account, you are able to customize a number of account settings for your data warehouse. These can be accessed by selecting your organization name in the upper right-hand corner of any screen, then choosing **Account Settings** from the dropdown.

* **Client Name:** This setting appears in the upper-right-hand corner of all dashboards and elsewhere throughout your account. If you want to change **"Vandelay Industries Co., Ltd"** to just **"Vandelay"**, this is where to do that.

* **Currency:** This is the *default currency* for all monetary values in your account. Anytime a decimal or currency value is synced into your data warehouse, this setting determines the symbol placed before that value within your reports.

* **Blackout Hours:** This setting ensures that, during the selected hours of the day, your data warehouse does not access your connected databases. All hours are expressed at zero-hour and in ET. For example, if you do not want your production database to be accessed between the hours of 9:00 AM EST and 1:00 PM EST, you should type the following array of digits: **9, 10, 11, 12**.

* **Forced update hours:** This setting ensures that a data warehouse update automatically begins in your account *on the hour(s)* you have specified. As with blackout hours, these are also in ET. For example, if you want data warehouse updates to begin automatically at **midnight** and **noon** ET, you should type the following array of digits: **0, 12**.

* **Send email summaries if the data has not updated yet:** This option tells the system what to do in situations where an email summary is scheduled to be sent *before the data in one of its reports* is refreshed up to the present. If you choose **No**, your account will skip sending the email at its scheduled time, and instead send it once your data has updated. If you choose **Yes**, your account will send the email, include a message explaining that the data is stale, and will send another email once your data has updated.

* **Enable data updates:** This option ensures that data updates run on your account. If you change the setting to **No**, data syncs and column calculations will completely halt in your account.

>[!NOTE]
>
>Make sure to select **Save Customizations** after you make any changes.

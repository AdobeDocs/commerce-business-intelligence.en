---
title: Manage your account settings
description: Learn how to customize your account settings for your Data Warehouse.
exl-id: 847d51b1-287e-4c14-b64e-0bd9bfcccedc
role: Admin, User
feature: Business Performance
---
# Customizing your account settings

>[!NOTE]
>
>Requires [Admin permissions.](../../administrator/user-management/user-management.md)

In your [!DNL Commerce Intelligence] account, you can customize your account settings for your Data Warehouse. These can be accessed by selecting your organization name in the upper right-hand corner of any screen, then choosing **[!UICONTROL Account Settings]** from the dropdown.

* **[!UICONTROL Client Name:]** This setting appears in the upper-right corner of all dashboards and elsewhere throughout your account. If you want to change **[!UICONTROL "Vandelay Industries Co., Ltd]** to just **[!UICONTROL "Vandelay]**, this is where to do that.

* **[!UICONTROL Currency:]** This is the *default currency* for all monetary values in your account. Anytime a decimal or currency value is synced into your Data Warehouse, this setting determines the symbol placed before that value within your reports.

* **[!UICONTROL Blackout Hours:]** This setting ensures that, during the selected hours of the day, your Data Warehouse does not access your connected databases. All hours are expressed at zero-hour and in Eastern Standard Time (EST). For example, if you do not want your production database to be accessed between the hours of 9:00 a.m. EST and 1:00 p.m. EST, you should type the following array of digits: **9, 10, 11, 12**.

* **[!UICONTROL Forced update hours:]** This setting ensures that a Data Warehouse update automatically begins in your account *during the hours* you have specified. As with blackout hours, these are also in ET. For example, if you want Data Warehouse updates to begin automatically at **midnight** and **noon** EST, you should type the following array of digits: **0, 12**.

* **[!UICONTROL Send email summaries if the data has not updated yet:]** This option manages situations when an email summary is scheduled to send *before the data in one of its reports* is refreshed. If you choose **No**, your account skips sending the email at its scheduled time. Instead, your account sends it once your data has updated. If you choose **[!UICONTROL Yes]**, your account sends the email, includes a message explaining that the data is stale, and sends another email once your data has updated.

* **[!UICONTROL Enable data updates:]** This option ensures that data updates run on your account. If you change the setting to **[!UICONTROL No]**, data syncs and column calculations halt in your account.

>[!NOTE]
>
>Make sure to select **[!UICONTROL Save Customizations]** after you make any changes.

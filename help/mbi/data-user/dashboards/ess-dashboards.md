---
title: Dashboards
description: Learn how to create and work with a dashboard.
---
# Dashboards

[!DNL MBI] Dashboards give you a quick view of your store's performance and sales activity at a glance. Individual dashboards can be shared with other users and organized into logical groups. You can also set different levels of permission for other users.

It is easy to create a new report, add it to a dashboard, and export the data to Excel. Charts and reports can be resized and dragged into position on the dashboard.

![Dashboard](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-holiday-sales-dashboard.png)

## Creating dashboards {#createdash}

Dashboards are essentially sharable, themed buckets for the analyses you create in the Report Builders. This is how you can encourage your team to collaborate and maintain a single source of truth across your organization.

*If you are an Admin or a Standard user*, you can create a dashboard by clicking the `Dashboard Options` dropdown and choosing `Create New dashboard`.

What the dashboards you create look like is entirely up to you. You can arrange and resize the elements in the dashboard any way you wish to suit your needs and workflow.

![arrange resize dashboard element](../../assets/arrange_resize_dashboard_element.gif)

### Create a new dashboard

1. On the menu, click **[!UICONTROL Dashboards]**.

1. The name of the default dashboard appears in the upper-left corner of the dashboard header. Click the down arrow (![](../../assets/magento-bi-btn-down.png)) to show the available options.

    ![Create Dashboard](../../assets/magento-bi-dashboard-create.png)

1. Click **[!UICONTROL Create Dashboard]**. Then, do the following:

    * Enter a `Name` for your dashboard.

    * To create a new `Group` for the dashboard, enter the name of the group.

        For example, if your [!UICONTROL Magento] installation has multiple store views, you might create a Group for each store view.

    * Click **[!UICONTROL Create]**.

    ![dashboard name](../../assets/magento-bi-dashboard-create-name.png)

    * The name of your new dashboard appears in the upper-left corner. Click the down arrow (![](../../assets/magento-bi-btn-down.png)) to show the options. If you created a group, the new dashboard appears below the group in the list.

### Add a report

1. To add a report, do one of the following:

    * Click the **[!UICONTROL Add a report]** prompt on the page.

    * In the dashboard header, click **[!UICONTROL Add Report]**.

        ![Add Report](../../assets/magento-bi-dashboard-create-add-report.png)

1. Click **[!UICONTROL Create Report]** to show the **[!UICONTROL Report Builder Options]**.

    ![Report Builder Options](../../assets/magento-bi-report-builder.png)

## Arrange items on a dashboard

* To resize a chart or report, drag the lower-right corner to the new size.

* To move a chart or report, hover over the title or header until the cursor changes to a cross. Then, drag it into position.

## Managing your dashboards {#managedash}

In **[!DNL Manage Data** > **Dashboards]**, you can manage user permissions for dashboards you own, delete dashboards you no longer need, and set a default dashboard.

### Sharing your dashboards {#sharingdash}

To truly scale [!DNL MBI] throughout your organization and provide valuable insights, we encourage you to share dashboards you create with other team members. *You can share dashboards you own* by clicking the `Share Dashboard` option at the top of the page.

When you share a dashboard, you can assign permissions across your organization OR on an individual basis, meaning you get to decide who can view and edit your reports.

>[!NOTE]
>
>`Read-Only` users only have access to dashboards that are directly shared with them - they are not able to search for and add dashboards on their own. Do not forget to keep them in the loop!

### Accessing shared dashboards {#accessshared}

*If you are an Admin or Standard user* and want to add a shared dashboard to your account, you can do so by clicking **[!UICONTROL Dashboard Options]** and then clicking **[!UICONTROL Find]** in the dropdown.

![find dashboard](../../assets/find_dashboard.png)<!--{: width="1000" height="535"}-->

### Manage dashboard settings

1. On the menu, click **[!DNL Manage Data** > **Dashboards]**.

1. If applicable, enter a new `Dashboard Name`.

1. To assign the dashboard to a specific `Dashboard Group`, choose from the list of groups.

    **`Permissions`**

    To give all users the same level of access to the dashboard, do the following:

    1. Under **`Shared with`**, choose one of the following options:

        * `View`
        * `Edit`
        * `None`

    1. When prompted for confirm, click **[!UICONTROL OK]** to update the permissions level for each user.

    1. To change the permission level of an individual, find the user in the list change the permission level. The change is automatically saved.

    **`Default`**

    1. To make this dashboard the default for your [!DNL MBI] account, click **[!UICONTROL Make Default]**.

    **`Remove`**

    1. To remove the dashboard, click **[!UICONTROL Delete Dashboard]**.

---
title: Share dashboards with other users
description: Learn how to share dashboards with other users.
exl-id: 6279b049-d1b2-4d40-b30b-ee8772e990f4
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
TQID: https://experienceleague.adobe.com/19tCk4327YLMnSrgQ0xHBinwiK2XHd7QU6l5rO-B6-k
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
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
---
# Share dashboards with other users

Sharing dashboards is a great way to keep your team in the loop and encourage collaborative discussion. By creating and sharing a central dashboard, you can provide your team with the information they need while still maintaining control. [[!DNL Adobe] recommends](../../best-practices/share-dashboard-best-practice.md){: target="_blank"} that you grant `Edit` rights to a select few to minimize accidental changes.

>[!NOTE]
>
>If the dashboard you are sharing contains reports built with metrics that a specific user does not have access to, the reports display an `Error Loading Data` message. If you want the data to appear to the specific user, an [admin user](../../administrator/user-management/user-management.md) must grant access to all metrics used in those reports.

## Share a dashboard

1. Click **[!UICONTROL Share Dashboard]** at the top of the screen.

   A list of all users in your [!DNL Commerce Intelligence] account will display.

1. To select a user to share the dashboard with, check the box to the left of their name.

   To select/deselect all users, click **[!UICONTROL Select]** and select `Everyone` or `None`, respectively.

1. Permissions can be set on a user-by-user basis or en masse.

    *To set individual permissions*, click **[!UICONTROL None]** to the right of the user's name. From this dropdown, select the type of permissions the user should have.

    *To set permissions en masse*, click **[!UICONTROL Set Permissions]**. From this dropdown, select the type of permissions the selected users should have.

    >[!NOTE]
    >
    >You can also use this feature to update previously set permissions. For example, if you want to stop sharing the dashboard with someone, set their permissions to `None`.

1. To share the dashboard, click **[!UICONTROL Save Changes]**. The selected user(s) will receive an email inviting them to view the dashboard.

Example:

![share dashboard](../../assets/Share_Dashboards.gif)

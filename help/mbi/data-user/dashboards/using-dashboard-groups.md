---
title: Use Dashboard Groups
description: Learn how to allow better organization of dashboards.
exl-id: e48b7345-62d0-4898-997e-3c3c02040ad3
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
---
# Use dashboard groups

Dashboard groups allow better organization of dashboards. The most common use case is to group similar dashboards under the same "group". For example, all dashboards related to marketing could be grouped under a dashboard group "Marketing".

In the dashboard selection dropdown, dashboard groups are shown in alphabetical order, with all dashboards under "No Group" shown last. Dashboards under the same group are shown together and in alphabetical order within each group.

## Dashboard Group Sharing

Dashboard groups cannot be directly shared between users. When a dashboard is shared with users, the dashboard group it is under is automatically created for those users if it does not exist. If the dashboard group exists, the dashboard is appended to the list.

When a dashboard's group is changed by its owner, the change is reflected automatically for all users with whom the dashboard has been shared. Users cannot change the dashboard group for dashboards they do not own.

## Create dashboard groups

Dashboard groups can be created in one of two ways:

1. When creating a dashboard:

   ![create dashboard group](../../assets/create-dashboard-groups-new-dashboard.png)

1. When changing the group of an existing dashboard, from the `Manage Data > Dashboards` page:

   1. Click the dashboard for which you would like to create the group.

   1. Under `Dashboard Group (optional)`, the current dashboard group appears.

   1. To create a group, type the name of the new group and then click outside the box.

      ![create dashboard group](../../assets/create-dashboard-groups-existing-dashboard.png)

## Add Existing Dashboards to Existing Groups

1. On the `Manage Data > Dashboards` page, choose the dashboard for which to change the group.

1. The text under `Dashboard Group (optional)` shows the current dashboard group of the dashboard.

1. To change the group of the dashboard, choose another group from the list – in this case `PS`, `Campaigns`.

   ![change group dashboard](../../assets/add-existing-dashboard-existing-group.png)

## Delete dashboard groups

When a dashboard group has no dashboards under it, it is automatically deleted.

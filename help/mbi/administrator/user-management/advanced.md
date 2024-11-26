---
title: Advanced user management
description: Enhance data visibility, streamline reporting, tailor access by user groups, simplify dashboard sharing, and ensure security and scalability for your organization.
role: Admin, User
feature: User Management
---

# Advanced user management

Advanced User Management provides enhanced data visibility controls and enables logical data filtering based on user groups (organizational regions).

Advanced User Management allows data visibility to be tailored based on user groups. It also eliminates the need to create a replica of existing dashboards to meet region-specific reporting requirements every time the business expands to a new region.

It simplifies dashboard sharing and data visibility while ensuring security and scalability for large organizations. The flexibility to configure user groups, roles, and permissions makes Commerce Intelligence a powerful tool for enterprise level requirements.

With Advanced User Management turned on, only the Admin user can create.

- Metrics
- Visual Report Builder
- SQL based Reports
- Email Summary
- Raw Exports

>[!NOTE]
>
>Admins can cross-collaborate by sharing dashboards with each other using Edit access.

## Feature matrix

Advanced User Management impacts several features across Commerce Intelligence. Below is a list of features, permissions, their availability for various roles based on the feature being turned on or off.

[table]

## Admin control

Admin users oversee:

- Configuring of user groups
- Assigning role and user group to individual users
- Sharing dashboards with user groups or other admins with dashboard level usage permissions
- Setting up of Email Summaries with user group level data filtering

### Configure user groups

User Groups are logical groupings of regions mapped to specific store filters. For example, user groups created based on names of continents, countries, and regions.

To configure user groups:

1. Go to Manage Users > User Groups, to view existing user groups.

   ![Configure user groups](../../assets/configure-user-groups.png)

1. Add Group allows creation of a new User Group
   
   - Provide a name for the group (e.g., "Americas")
   
   - Select stores or filters relevant to the group

   - Save the configuration

     ![Add user groups](../../assets/add-group.png)

1. Editing or deleting groups

   - Groups can be edited anytime to update store mappings or renamed for clarity.

   - Delete user groups when they are not required for your business. This means, the existing users mapped to this group need to be reassigned manually.

1. Default groups:

   - "None" Group: A fallback group for users not yet mapped to a specific group. These users won't see any data until assigned to an appropriate group.

   - "All" Group: Provides unrestricted access to all data, typically reserved for admin users.

### Assign users to user groups

New users can be mapped to relevant groups during their onboarding by using Invite a User. Existing users can be remapped to user groups based on business requirement.

![Assign users to user groups](../../assets/assign-users-to-groups.png)

Tip: Till a Standard or Read-only user is assigned to a relevant user group, it is safe to assign them to 'None' to ensure they don't access any dashboards data mistakenly.

Tip: During assignment of permissions to a user, based on business requirement, there is a possibility of restricting specific stores within a group for an enhanced control.

Note: Admin users always are mapped to 'All' stores by default that allows them to view dashboards with full store view.

### Share dashboards

Advanced User Management provides powerful options for sharing dashboards while maintaining data security.

- Dashboards can be shared with the user groups as well as with other admin users. This enables a centralized management of dashboards thereby simplifying management for large organizations.

   ![Share dashboards](../../assets/share-dashboards.png)

- Dashboard sharing permissions include:  

   - Edit: Made available only for Admin users to modify the dashboard, filter its data, modify reports or export data

   - View: Available to users across all roles with certain restrictions

   - None: Revokes access to the dashboard for certain user groups or Admins

   Note: Please refer to the system behavior summary sheet above, for usability of various Commerce Intelligence features as per the rule & dashboard permissions to understand various combinations.

#### Consumption of shared dashboards

Admin user can view the dashboard data with access to all the stores.

![View dashboard admin](../../assets/view-dashboard-admin.png)

Whereas, the users consuming the shared dashboard can view the dashboards with data filtered as per the stores that are mapped to them during user configuration.

![View dashboard admin](../../assets/view-dashboard-user.png)

>[!TIP]
>
>There is an added flexibility of enabling date filters. This means, shared dashboards can be viewed with different date range instead of the default time span specified for individual reports during their creation. It can be turned on or off based on the business requirement.

### Schedule email summaries  

Advanced User Management extends its data filtering capabilities to email summaries. Depending on the email audience, the Admin users can specify the user groups for which the selected reports must be filtered.

![Schedule email summary](../../assets/schedule-email-summary.png)

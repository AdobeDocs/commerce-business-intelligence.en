---
title: Managing users and permissions
description: Learn how to manage your [!DNL MBI] users. 
---
# Manage user permissions

MBI is intended to be a single source of truth across your organization. Each user will have their own set of dashboards which they can [share with other users](../../data-user/dashboards/share-dashboard-with-users.md).

## User Permission Levels

In MBI, there are three general permission levels that apply to users, which are selected when an account is created:

* Admin
* Standard
* Read-Only

These permissions enable users to perform certain actions or access specific parts of Magento Business Intelligence. Here's a table of what each permission level can do in Magento Business Intelligence:

|   | Admin | Standard | Read Only |
| -----|-----|-----|----|
| **Create/manage users** | ✔|   |   |
| **Create email summaries** | ✔ | ✔ |   |
| **Create/edit/share dashboards** | ✔ | ✔ |   |
| **View dashboards** | ✔ | ✔ | ✔ |
| **Create/edit/delete visual reports** | ✔ | ✔* |   |
| **Create/edit/delete SQL reports** | ✔ |  |   |
| **Clone dashboards** | ✔ |   |   |
| **Add/manage integrations** | ✔ |   |   |
| **Access the Data Warehouse Manager** | ✔ |   |   |
| **Sync/unsync tables and columns** | ✔ |   |   |
| **Create/edit metrics** | ✔ |   |   |
| **Create/edit filter sets** | ✔ |   |   |
| **Create/edit calculated columns** | ✔ |   |   |
| **Create list of dependent reports** | ✔ |   |   |
| **Access System Summary** | ✔ |   |   |
| **Access Timezone settings** | ✔ |   |   |
| **Access Billing** | ✔ | ✔** |   |
| **Contact Support** | ✔ | ✔ | ✔ |

{style="table-layout:auto"}

>[!NOTE]
>
>_You can limit a Standard user's [access to specific metrics](../../administrator/user-management/restrict-metric-access.md)._
>
>_Standard users can access Billing with an additional permission setting._
>
>Read-Only users can only _view_ dashboards that have been shared with them; they cannot create or edit anything in MBI, nor can they search for and add new dashboards to their account. We recommend that you share a specific set of dashboards with Read-Only users that you or another member of your team maintains. Do not clone a set of dashboards for them.

## Additional permissions: Billing and Technical {#billingtech}

In addition to the general permission levels, two other user designations also exist - Billing and Technical. These designations are intended to be used in conjunction with the general permission levels.

### Billing

Billing users have access to the billing page and can change payment information. Additionally, they may also be contacted by our teams for billing questions.

Admin users have access to the Billing tab by default, but Standard users can also gain access if they have the 'Billing' checkbox selected on their profile.

![billing](../../assets/billing.png)<!--{: width="550" height="363"}-->

### Technical

Technical users do not have any permissions specific to them - this setting just marks a technical contact within your organization. These users may be contacted by our teams for technical questions.

Admins can add new users to their account by clicking **Account Settings > Create Users** and following the prompts. After the user is created in MBI, the lucky person you are inviting will receive email instructions on how to complete the account setup process.

At any time, Admins can view all the users in their account by clicking **Account Settings > Manage Users**. This page displays the user's permissions and what metrics and dashboards they have access to.

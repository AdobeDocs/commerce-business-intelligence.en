---
title: Expected Zendesk data
description: Learn the main data tables that you can import from Zendesk into Commerce Intelligence, including links to additional documentation about Zendesk data.
exl-id: 838d8d13-e2e1-44c2-a416-f1792200ee6f
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
---
# Expected [!DNL Zendesk] data

After [you have connected your [!DNL Zendesk] account](../integrations/zendesk.md), you can use the [Data Warehouse Manager](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) to easily track relevant data fields for analysis.

This topic explores the main data tables that you can import from [!DNL Zendesk] into [!DNL Adobe Commerce Intelligence], including links to additional documentation about [!DNL Zendesk] data.

| Table name | Description |
|-----|-----|
| [`Audits`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits) | The `Audits` table records activity associated with a ticket, including status changes and both customer and agent responses. This table includes a ticket id which links back to the `Tickets` table, which allows you to analyze the time to first response and time to resolution for each ticket. |
| [`Audit_~\_Events`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits#audit-events) | The `audit_~\_events` table is the child of the `audits` table and records additional details of a ticket event. |
| [`Organizations`](https://developer.zendesk.com/rest_api/docs/core/organizations) | The `Organizations` table records company information about your end-users such as the name, ID, associated domain names, tags, and any custom fields. |
| [`Tickets`](https://developer.zendesk.com/rest_api/docs/core/tickets) | The `Tickets` table records all ticket details, including the `created_at` timestamp and the `requester\_id` and `assignee\_id`, which allows you to link a ticket to an end-user and agent in the `Users` table respectively. |
| [`Ticket_~\_Fields`](https://developer.zendesk.com/rest_api/docs/core/ticket_fields) | The `ticket fields` table contains information about the basic text fields and custom ticket fields in your account. Attributes of this table include the field `ID`, `URL`, `type`, `title`, `description`, `position`, `requirement setting`, agent and end-user-specific information, and creation and update information. |
| [`Users`](https://developer.zendesk.com/rest_api/docs/core/users) | The `Users` table includes all details on end-users and agents, including the individual's name and email. This allows you to analyze both the engagement of your end-users and the performance of your agents. |
| [`Zendesk\_Groups`](https://developer.zendesk.com/rest_api/docs/core/groups) | Groups are how agents are organized in your Zendesk account. The `Groups` table records information such as the `group ID`, `URL`, `name`, and creation and update information. |
| [`Zendesk\_Macro`](https://developer.zendesk.com/rest_api/docs/core/macros) | Macros are actions defined by you that modify the values of a ticket's fields. This table contains attributes such as the macro's title, ID, actions, restrictions, and creation and update information. |
| [`Zendesk\_Tags`](https://developer.zendesk.com/rest_api/docs/core/tags) | The `Tags` table contains a list of all the tags in your account. |
| [`Zendesk\_Ticket\_Metrics`](https://developer.zendesk.com/rest_api/docs/core/ticket_metrics#ticket-metrics) | This table contains data about ticket metrics. Fields include the `ticket ID`, `URL`, and the number of groups, assignees, reopens, replies, reply time (in minutes), full resolution time, and last update (for example, status, assignee, or requester) information. |

{style="table-layout:auto"}

## Related

* [Connecting Zendesk](../integrations/zendesk.md)
* [Reauthenticating integrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)

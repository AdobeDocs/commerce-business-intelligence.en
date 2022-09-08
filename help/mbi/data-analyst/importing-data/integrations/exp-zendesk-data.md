---
title: Expected Zendesk data
zendesk_id: 360016733291
---

After [you’ve connected your Zendesk account](../data-analyst/importing-data/integrations/zendesk.md), you can use the [Data Warehouse Manager](../{{ site.baseurl }}/data-analyst/data-warehouse-mgr/tour-dwm.html#syncing) to easily track relevant data fields for analysis.

In this article, we’ll explore the main data tables that you can import from Zendesk into MBI, including links to additional documentation about Zendesk data.

| Table name | Description |
| [Audits](https://developer.zendesk.com/rest_api/docs/core/ticket_audits) | The **audits** table records activity associated with a ticket, including status changes and both customer and agent responses. This table includes a ticket\_id which links back to the **tickets** table, which allows you to analyze the time to first response and time to resolution for each ticket. |
| [Audit\_~\_Events](https://developer.zendesk.com/rest_api/docs/core/ticket_audits#audit-events) | The **audit\_~\_events** table is the child of the **audits** table and records additional details of a ticket event. |
| [Organizations](https://developer.zendesk.com/rest_api/docs/core/organizations) | The organizations table records company information about your end-users such as the name, ID, associated domain names, tags, and any custom fields. |
| [Tickets](https://developer.zendesk.com/rest_api/docs/core/tickets) | The **tickets** table records all ticket details, including the created_at timestamp as well as the requester\_id and assignee\_id, which allows you to link a ticket to an end-user and agent in the **users** table respectively. |
| [Ticket\_~\_Fields](https://developer.zendesk.com/rest_api/docs/core/ticket_fields) | The **ticket fields** table contains information about the basic text fields as well as custom ticket fields in your account. Attributes of this table include the field ID, URL, type, title, description, position, requirement setting, agent and end-user specific information, and creation and update information. |
| [Users](https://developer.zendesk.com/rest_api/docs/core/users) | The **users** table includes all details on end-users and agents, including the individual’s name and email. This allows you to analyze both the engagement of your end-users as well as the performance of your agents. |
| [Zendesk\_Groups](https://developer.zendesk.com/rest_api/docs/core/groups) | Groups are how agents are organized in your Zendesk account. The **groups** table records information such as the group ID, URL, name, and creation and update information. |
| [Zendesk\_Macro](https://developer.zendesk.com/rest_api/docs/core/macros) | Macros are actions defined by you that modify the values of a ticket's fields. This table contains attributes such as the macro's title, ID, actions, restrictions, and creation and update information. |
| [Zendesk\_Tags](https://developer.zendesk.com/rest_api/docs/core/tags) | The **tags** table contains a list of all the tags in your account. |
| [Zendesk\_Ticket\_Metrics](https://developer.zendesk.com/rest_api/docs/core/ticket_metrics#ticket-metrics) | This table contains data about (you guessed it) ticket metrics. Fields include the ticket ID, URL, and the number of groups, assignees, reopens, replies, reply time (in minutes), full resolution time, and last update (status, assignee, requester, etc) information. |

### Related

* [Connecting Zendesk](../data-analyst/importing-data/integrations/zendesk.md)
* [Reauthenticating integrations](https://support.magento.com/hc/en-us/articles/360016733151-Reauthenticating-integrations)


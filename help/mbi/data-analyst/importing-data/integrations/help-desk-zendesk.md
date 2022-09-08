---
title: Help desk reporting for Zendesk
zendesk_id: 360016507092
---

{:.bs-callout-info}
This is only available for clients that are on the Pro plan and utilizing the new architecture. You are on the [new architecture](https://support.magento.com/hc/en-us/articles/360016503052-New-Architecture-FAQ) if you have the \"Data Warehouse Views\" section available after selecting \"Manage Data\" from the main toolbar.

Consolidating your Zendesk data with your transactional database is an excellent way to better understand how your customers are interacting with your sales or customer success teams and what type of customers are utilizing your support platform. In this article, we will demonstrate how to set up a dashboard to get granular reports about your Zendesk performance and tie in your transactional customers.

Before getting started, you\'ll want to connect your [Zendesk](../data-analyst/importing-data/integrations/zendesk.md). This analysis contains [advanced calculated columns](../data-analyst/data-warehouse-mgr/adv-calc-columns.md).

<!-- Getting Started -->

## Getting Started

### Columns to track

* **`audits`** table
* **`_id`**
* **`created_at`**
* **`id`**
* **`ticket_id`**
* **`_updated_at`**
{: style="list-style-type: circle;"}

* **`audits_~_events`** table
* **`_sub_id`**
* **`_id_of_parent`**
* **`author_id`**
* **`field_name`**
* **`public`**
* **`type`**
* **`value`**
{: style="list-style-type: circle;"}

* **`tickets`** table
* **`_id`**
* **`assignee_id`**
* **`created_at`**
* **`id`**
* **`requester_id`**
* **`status`**
* **`updated_at`**
* **`via_~_source_~_from_~_address`**
* **`_updated_at`**
{: style="list-style-type: circle;"}

* **`users`** table
* **`_id`**
* **`created_at`**
* **`emails`**
* **`id`**
* **`role`**
* **`updated_at`**
* **`_updated_at`**
{: style="list-style-type: circle;"}

### Filter sets to create

* **`[Zendesk] Tickets`** table
  * status != deleted
  {: style="list-style-type: circle;"}

* Filter set name: Tickets we count
* Filter set logic:
{: style="list-style-type: circle;"}

## Calculated Columns

### Columns to create

* **`[Zendesk] user's`** table
  * **`User is agent? (Yes/No) `**
  * * **Column type** - "Same Table -&gt; Calculation"

    * **Input columns** - `role`, `email`

    *  **SQL** **Calculation** - `case when A is not null and A!='end-user' then 'Yes' when B is not null and B like '%@magento.com' then 'Yes' else 'No' end`

    * Replace '@magento.com' with your domain

    * **Datatype** - String

* **`[Zendesk] audits_~_events`** table
  * Select a definition: Joined Column
  * Create Path:
  * Many: [Zendesk] audits_~_events.author_id
  * One: [Zendesk] users.id

  * Select table: **`[Zendesk] users`**
  * Select column: **`User is agent? (Yes/No)`**
  * Path: [Zendesk] audits_~_events.author_id = [Zendesk] users.id
  {: style="list-style-type: square;"}

* **`Author is agent? (Yes/No)`**
{: style="list-style-type: circle;"}

* **`[Zendesk] audits`** table
  * Select a definition: Exists
  * Create Path:
  * Many: [Zendesk] audits_~_events._id_of_parent
  * One: [Zendesk] audits._id

  * Select table: **`[Zendesk] audits_~_events`**
  * Path: [Zendesk] audits_~_events._id_of_parent = [Zendesk] audits._id
  * Filter:
  * field_name = status
  * type = Change
  * value = solved
  {: style="list-style-type: square;"}

  * Select a definition: Exists
  * Select table: **`[Zendesk] audits_~_events`**
  * Path: [Zendesk] audits_~_events._id_of_parent = [Zendesk] audits._id
  * Filter:
  * Author is agent? (Yes/No)
  * type = Comment
  * public = 1
  {: style="list-style-type: square;"}

* **`Status changes to solved? (1/0)`**
* **`Is agent comment? (1/0)`**
{: style="list-style-type: circle;"}

* **`[Zendesk] Tickets`** table
  * Select a definition: Joined Column
  * Create Path:
  * Many: [Zendesk] tickets.requester_id
  * One: [Zendesk] users.id

  * Select table: **`[Zendesk] users`**
  * Select column: **`email`**
  * Path: [Zendesk] tickets.requester_id = [Zendesk] users.id
  {: style="list-style-type: square;"}

  * Select a definition: Joined Column
  * Select table: **`[Zendesk] users`**
  * Select column: **`role`**
  * Path: [Zendesk] tickets.requester_id = [Zendesk] users.id
  {: style="list-style-type: square;"}

  * Select a definition: Max
  * Create Path:
  * Many: [Zendesk] audits.ticket_id
  * One: [Zendesk] tickets.id

  * Select table: **`[Zendesk] audits`**
  * Select column: **`created_at`**
  * Path: [Zendesk] audits.ticket_id = [Zendesk] tickets.id
  * Filter:
  * status changed to solved = 1
  {: style="list-style-type: square;"}

  * Select a definition: Min
  * Select table: **`[Zendesk] audits`**
  * Select column: **`created_at`**
  * Path: [Zendesk] audits.ticket_id = [Zendesk] tickets.id
  * Filter:
  * Is agent comment? = 1
  {: style="list-style-type: square;"}

* **`Requester's email`**
* **`Requester's role`**
* **`Ticket's latest solved date`**
* **`First agent response date`**
* **``** **`Seconds to resolution`**
  * * **Column type** - "Same Table -&gt; Date Difference"

    * `Ticket's latest solved date` minus `created_at`
  {: style="list-style-type: circle;"}

* **`Seconds to first response`**
  * * **Column type** - "Same Table -&gt; Date Difference"

    * `First agent response date` minus `created_at`
  {: style="list-style-type: circle;"}

* **``****`Requester's ticket number `**
  * * **Column type** - "Same Table -&gt; Event Number"

    * **Event Owner** - `requester_id`

    * **Event Rank** - `created_at`
  {: style="list-style-type: circle;"}

* **``****`Ticket created_at (hour of day)`**
  * * **Column type** - "Same Table -&gt; Calculation"

    * **Input columns** - `created_at`

    * **SQL Calculation** - `to_char(A,'HH24')::int

    * **Datatype** – Integer
  {: style="list-style-type: circle;"}

* **``****`Ticket created_at (day of week)`**
  * * **Column type** - "Same Table -&gt; Calculation"

    * **Input columns** - `created_at`

    * **Calculation** - `to_char(A,'D')||'. '||to_char(A,'Day')`

    * **Datatype** – String
  {: style="list-style-type: circle;"}
{: style="list-style-type: circle;"}

* **`customer_entity`** table
  * Select a definition: Count
  * Create Path:
  * Many: [Zendesk] tickets.email
  * One: customer_entity.email

  * Select table: **`[Zendesk] tickets`**
  * Path: [Zendesk] tickets.email = customer_entity.email
  * Filter:
  * Tickets we count
  {: style="list-style-type: square;"}

* **`User's lifetime number of support tickets requested`**
* **``****`Has user filed a support ticket? (Yes/No)`**
  * * **Column type** - "Same Table -&gt; Calculation"

    * **Input columns** - `User's lifetime number of support tickets requested`

    * **Calculation** - `case when A&gt;0 then 'Yes' else 'No' end`

    * **Datatype** – String
  {: style="list-style-type: circle;"}
{: style="list-style-type: circle;"}

* **`[Zendesk] Tickets`** table
  * Select a definition: Joined Column
  * Select table: **`customer_entity`**
  * Select column: **`User's lifetime number of support tickets requested`**
  * Path: [Zendesk] tickets.email = customer_entity.email
  {: style="list-style-type: square;"}

* **`Requester's lifetime number of support tickets`**
{: style="list-style-type: circle;"}

## Metrics

* **[Zendesk] New tickets**
  * Tickets we count
  {: style="list-style-type: square;"}

* In the **`[Zendesk] tickets`** table
* This metric performs a **Count**
* On the **`id`** column
* Ordered by the **`created_at`** timestamp
* Filter:
{: style="list-style-type: circle;"}

* **[Zendesk] Solved tickets**
  * Tickets we count
  * status IN closed, solved
  {: style="list-style-type: square;"}

* In the **`[Zendesk] tickets`** table
* This metric performs a **Count**
* On the **`id`** column
* Ordered by the **`created_at`** timestamp
* Filter:
{: style="list-style-type: circle;"}

* **[Zendesk] Distinct users filing tickets**
  * Tickets we count
  {: style="list-style-type: square;"}

* In the **`[Zendesk] tickets`** table
* This metric performs a **Count Distinct**
* On the **`requester_id`** column
* Ordered by the **`created_at`** timestamp
* Filter:
{: style="list-style-type: circle;"}

* **[Zendesk] Average/median ticket resolution time**
  * Tickets we count
  * status IN closed, solved
  {: style="list-style-type: square;"}

* In the **`[Zendesk] tickets`** table
* This metric performs an **Average (or Median)**
* On the **`Seconds to resolution`** column
* Ordered by the **`created_at`** timestamp
* Filter:
{: style="list-style-type: circle;"}

* **[Zendesk] Average/median time to first response**
  * Tickets we count
  * status IN closed, solved
  {: style="list-style-type: square;"}

* In the **`[Zendesk] tickets`** table
* This metric performs an **Average (or Median)**
* On the **`Seconds to first response`** column
* Ordered by the **`created_at`** timestamp
* Filter:
{: style="list-style-type: circle;"}

{:.bs-callout-info}
Make sure to [add all new columns as dimensions to metrics](../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) before building new reports.

#### Reports

* **New/Open/Pending tickets**
  * Metric: New Tickets
  * Filter:
  * status IN new, open, pending
  {: style="list-style-type: square;"}

* *Metric A: New tickets*
* *Time period: All time*
* *Interval: None*
* *Chart Type: Scalar*
{: style="list-style-type: circle;"}

* **Closed/Solved tickets**
  * Metric: New Tickets
  * Filter:
  * status IN solved, closed
  {: style="list-style-type: square;"}

* *Metric A: New tickets*
* *Time period: All time*
* *Interval: None*
* *Chart Type: Scalar*
{: style="list-style-type: circle;"}

* **Average time to first response**
  * Metric: Average time to first response
  {: style="list-style-type: square;"}

* *Metric A: Average time to first response*
* *Time period: All time*
* *Interval: None*
* *Chart Type: Scalar*
{: style="list-style-type: circle;"}

* **Average time to resolution**
  * Metric: Average time to resolution
  * Filter:
  * status IN solved, closed
  {: style="list-style-type: square;"}

* *Metric A: Averae time to resolution*
* *Time period: All time*
* *Interval: None*
* *Chart Type: Scalar*
{: style="list-style-type: circle;"}

* **Tickets by status**
  * Metric: New Tickets
  {: style="list-style-type: square;"}

* *Metric A: New tickets*
* *Time period: All time*
* *Interval: Monthly*
* *Group by: status*
* *Chart Type: Stacked Column*
{: style="list-style-type: circle;"}

* **Number of new and solved tickets**
  * Metric: New Tickets
  {: style="list-style-type: square;"}

  * Metric: New Tickets
  {: style="list-style-type: square;"}

* *Metric A: New tickets*
* *Metric B: Solved tickets*
* *Time period: All time*
* *Interval: Monthly*
* *Chart Type: Line*
{: style="list-style-type: circle;"}

* **Time to first response**
  * Metric: Average time to first response
  {: style="list-style-type: square;"}

* *Metric A: Average time to first response*
* *Time period: All time*
* *Interval: Monthly*
* *Chart Type: Column*
{: style="list-style-type: circle;"}

* **Time to resolution**
  * Metric: Average time to resolution
  * Filter:
  * status IN solved, closed
  {: style="list-style-type: square;"}

* *Metric A: Averae time to resolution*
* *Time period: All time*
* *Interval: Monthly*
* *Chart Type: Column*
{: style="list-style-type: circle;"}

* **Distinct users filing tickets**
  * Metric: Distinct users filing tickets
  {: style="list-style-type: square;"}

* *Metric A: Distinct users filing tickets*
* *Time period: All time*
* *Interval: Monthly*
* *Chart Type: Column*
{: style="list-style-type: circle;"}

* **Peak ticket days**
  * Metric: New Tickets
  {: style="list-style-type: square;"}

* *Metric A: New tickets*
* *Time period: All time*
* *Interval: None*
* *Group by: Ticket created_at (day of week)*
* *Chart Type: Pie*
{: style="list-style-type: circle;"}

* **Peak ticket hours**
  * Metric: New Tickets
  {: style="list-style-type: square;"}

  * Show top/bottom: Top 100% sorted by created_at (hour of the day)

* *Metric A: New tickets*
* *Time period: All time*
* *Interval: None*
* *Group by: Ticket created_at (hour of the day)*
* *Chart Type: Pie*
{: style="list-style-type: circle;"}

* **Avg LTV of users who have and have not filed tickets**
  * Metric: Average lifetime revenue
  {: style="list-style-type: square;"}

* *Metric A: Average lifetime revenue*
* *Time period: All time*
* *Interval: Monthly*
* *Group by: User has filed a support ticket?*
* *Chart Type: Column*
{: style="list-style-type: circle;"}

* **Number of new users who have and have not filed tickets**
  * Metric: Users
  {: style="list-style-type: square;"}

* *Metric A: New users*
* *Time period: All time*
* *Interval: Monthly*
* *Group by: User has filed a support ticket?*
* *Chart Type: Column*
{: style="list-style-type: circle;"}

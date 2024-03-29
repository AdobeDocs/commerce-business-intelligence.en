---
title: Help desk reporting for Zendesk
description: Learn about your most valued referral channels.
exl-id: b6142ef2-2be8-401f-ac35-f86fc68d204e
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
---
# Help desk reporting for [!DNL Zendesk]

>[!NOTE]
>
>This is only available for clients that are on the `Pro` plan and using the new architecture. You are on the new architecture if you have the `Data Warehouse Views` section available after selecting `Manage Data` from the main toolbar.

Consolidating your [!DNL Zendesk] data with your transactional database is an excellent way to better understand how your customers are interacting with your sales or customer success teams. It also helps you know what type of customers are using your support platform. This topic demonstrates how to set up a dashboard to get granular reports about your [!DNL Zendesk] performance and tie in your transactional customers.

Before getting started, you want to connect your [[!DNL Zendesk]](../integrations/zendesk.md). This analysis contains [advanced calculated columns](../../data-warehouse-mgr/adv-calc-columns.md).

<!-- Getting Started -->

## Getting Started

### Columns to track

* `audits` table
* `_id`
* `created_at`
* `id`
* `ticket_id`
* `_updated_at`

* `audits_~_events` table
* `_sub_id`
* `_id_of_parent`
* `author_id`
* `field_name`
* `public`
* `type`
* `value`

* `tickets` table
* `_id`
* `assignee_id`
* `created_at`
* `id`
* `requester_id`
* `status`
* `updated_at`
* `via_~_source_~_from_~_address`
* `_updated_at`

* `users` table
* `_id`
* `created_at`
* `emails`
* `id`
* `role`
* `updated_at`
* `_updated_at`

### Filter sets to create

* `[!DNL Zendesk] Tickets` table
  * `status != deleted`

* `Filter set name`: `Tickets we count`
* `Filter set logic`:

## Calculated Columns

### Columns to create

* **`[!DNL Zendesk] user's`** table
  * `User is agent? (Yes/No) `
  * * `Column type` - `Same Table > Calculation`

    * `Input columns` - `role`, `email`

    *  `SQL Calculation` `- case when `A` is not `null` and `A!=`end-user` then `Yes` when `B` is not `null` and `B` like `%@magento.com` then `Yes` else `No` end

    * Replace `@magento.com` with your domain

    * `Datatype` - `String`

* **`[!DNL Zendesk] audits_~_events`** table
  * Select a definition: `Joined Column`
  * [!UICONTROL Create Path]:
  * [!UICONTROL Many]: `[!DNL Zendesk] audits_~_events.author_id8`
  * [!UICONTROL One]: `[!DNL Zendesk] users.id`

  * Select a [!UICONTROL table]: `[!DNL Zendesk] users`
  * Select a [!UICONTROL column]: `User is agent? (Yes/No)`
  * [!UICONTROL Path]: `[!DNL Zendesk] audits_~_events.author_id = [!DNL Zendesk] users.id`

* **`Author is agent? (Yes/No)`**

* **`[!DNL Zendesk] audits`** table
  * Select a definition: `Exists`
  * [!UICONTROL Create Path]:
  * [!UICONTROL Many]: `[!DNL Zendesk] audits_~_events._id_of_parent`
  * [!UICONTROL One]: `[!DNL Zendesk] audits._id`

  * Select a [!UICONTROL table]: `[!DNL Zendesk] audits_~_events`
  * [!UICONTROL Path]: `[!DNL Zendesk] audits_~_events._id_of_parent = [!DNL Zendesk] audits._id`
  * [!UICONTROL Filter]:
  * `field_name` = `status`
  * `type` = `Change`
  * `value` = `solved`

  * Select a definition: `Exists`
  * Select a [!UICONTROL table]: `[!DNL Zendesk] audits_~_events`
  * [!UICONTROL Path]: `[!DNL Zendesk] audits_~_events._id_of_parent = [!DNL Zendesk] audits._id`
  * [!UICONTROL Filter]: `Author is agent? (Yes/No)`
  * `type` = `Comment`
  * `public` = `1`

* **`Status changes to solved? (1/0)`**
* **`Is agent comment? (1/0)`**

* **`[!DNL Zendesk] Tickets`** table
  * Select a definition: `Joined Column`
  * [!UICONTROL Create Path]:
  * [!UICONTROL Many]: `[!DNL Zendesk] tickets.requester_id`
  * [!UICONTROL One]: `[!DNL Zendesk] users.id`

  * Select a [!UICONTROL table]: `[!DNL Zendesk] users`
  * Select a [!UICONTROL column]: `email`
  * [!UICONTROL Path]: `[!DNL Zendesk] tickets.requester_id = [!DNL Zendesk] users.id`

  * Select a definition: `Joined Column`
  * Select a [!UICONTROL table]: `[!DNL Zendesk] users`
  * Select a [!UICONTROL column]: `role`
  * [!UICONTROL Path]: `[!DNL Zendesk] tickets.requester_id = [!DNL Zendesk] users.id`

  * Select a definition: `Max`
  * [!UICONTROL Create Path]:
  * [!UICONTROL Many]: `[!DNL Zendesk] audits.ticket_id`
  * [!UICONTROL One]: `[!DNL Zendesk] tickets.id`

  * Select a [!UICONTROL table]: `[!DNL Zendesk] audits`
  * Select a [!UICONTROL column]: `created_at`
  * [!UICONTROL Path]: `[!DNL Zendesk] audits.ticket_id = [!DNL Zendesk] tickets.id`
  * [!UICONTROL Filter]:
  * `status` changed to `solved = 1`

  * Select a definition: `Min`
  * Select a [!UICONTROL table]: `[!DNL Zendesk] audits`
  * Select a [!UICONTROL column]: `created_at`
  * [!UICONTROL Path]: `[!DNL Zendesk] audits.ticket_id = [!DNL Zendesk] tickets.id`
  * [!UICONTROL Filter]:
  * `Is agent comment? = 1`

* `Requester's email`
* `Requester's role`
* `Ticket's latest solved date`
* `First agent response date`
* `Seconds to resolution`
  * * `Column type` - `Same Table > Date Difference`

    * `Ticket's latest solved date` minus `created_at`

* **`Seconds to first response`**
  * * `Column type` - `Same Table > Date Difference`

    * `First agent response date` minus `created_at`

* **`Requester's ticket number`**
  * * `Column type` - `Same Table > Event Number`

    * `Event Owner` - `requester_id`

    * `Event Rank` - `created_at`

* **`Ticket created_at (hour of day)`**
  * * `Column type` - "Same Table > Calculation"

    * `Input columns` - `created_at`

    * `SQL Calculation` - `to_char(A,'HH24')::int`

    * `Datatype` – Integer

* **`Ticket created_at (day of week)`**
  * * `Column type` - "Same Table > Calculation"

    * `Input columns` - `created_at`

    * `Calculation` - `to_char(A,'D')||'. '||to_char(A,'Day')`

    *`Datatype` – `String`

* **`customer_entity`** table
  * Select a definition: `Count`
  * [!UICONTROL Create Path]:
  * [!UICONTROL Many]: `[!DNL Zendesk] tickets.email`
  * [!UICONTROL One]: `customer_entity.email`

  * Select a [!UICONTROL table]: `[!DNL Zendesk] tickets`
  * [!UICONTROL Path]: `[!DNL Zendesk] tickets.email = customer_entity.email`
  * [!UICONTROL Filter]:
  * `Tickets we count`

* **`User's lifetime number of support tickets requested`**
* **`Has user filed a support ticket? (Yes/No)`**
  * * `Column type` - "Same Table > Calculation"

    * `Input columns` - `User's lifetime number of support tickets requested`

    * `Calculation` - `case when A>0 then 'Yes' else 'No' end`

    * `Datatype` – `String`

* **`[!DNL Zendesk] Tickets`** table
  * Select a definition: `Joined Column`
  * Select a [!UICONTROL table]: `customer_entity`
  * Select a [!UICONTROL column]: `User's lifetime number of support tickets requested`
  * [!UICONTROL Path]: `[!DNL Zendesk] tickets.email = customer_entity.email`

* **`Requester's lifetime number of support tickets`**

## Metrics

* **[!DNL Zendesk] New tickets**
  * `Tickets we count`

* In the **`[!DNL Zendesk] tickets`** table
* This metric performs a **Count**
* On the **`id`** column
* Ordered by the **`created_at`** timestamp
* [!UICONTROL Filter]:

* **[!DNL Zendesk] Solved tickets**
  * `Tickets we count`
  * status IN `closed, solved`

* In the **`[!DNL Zendesk] tickets`** table
* This metric performs a **Count**
* On the **`id`** column
* Ordered by the **`created_at`** timestamp
* [!UICONTROL Filter]:

* **[!DNL Zendesk] Distinct users filing tickets**
  * `Tickets we count`

* In the **`[!DNL Zendesk] tickets`** table
* This metric performs a **Count Distinct**
* On the **`requester_id`** column
* Ordered by the **`created_at`** timestamp
* [!UICONTROL Filter]:

* **[!DNL Zendesk] Average/median ticket resolution time**
  * `Tickets we count`
  * status IN `closed, solved`

* In the **`[!DNL Zendesk] tickets`** table
* This metric performs an **Average (or Median)**
* On the **`Seconds to resolution`** column
* Ordered by the **`created_at`** timestamp
* [!UICONTROL Filter]:

* **[!DNL Zendesk] Average/median time to first response**
  * Tickets that are counted
  * status IN closed, solved

* In the **`[!DNL Zendesk] tickets`** table
* This metric performs an **Average (or Median)**
* On the **`Seconds to first response`** column
* Ordered by the **`created_at`** timestamp
* [!UICONTROL Filter]:

>[!NOTE]
>
>Make sure to [add all new columns as dimensions to metrics](../../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) before building new reports.

### Reports

* **[!UICONTROL New/Open/Pending tickets]**
  * [!UICONTROL Metric]: `New Tickets`
  * [!UICONTROL Filter]:
  * status IN `new, open, pending`

* Metric `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Closed/Solved tickets]**
  * [!UICONTROL Metric]: `New Tickets`
  * [!UICONTROL Filter]:
  * status IN `solved, closed`

* Metric `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Average time to first response]**
  * [!UICONTROL Metric]: `Average time to first response`

* Metric `A`: `Average time to first response`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Average time to resolution]**
  * [!UICONTROL Metric]: `Average time to resolution`
  * [!UICONTROL Filter]:
  * status IN `solved, closed`

* Metric `A`: `Average time to resolution`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Tickets by status]**
  * [!UICONTROL Metric]: `New Tickets`

* Metric `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Group by`: `status`
* `Chart Type`: `Stacked Column`

* **[!UICONTROL Number of new and solved tickets]**
  * [!UICONTROL Metric]: `New Tickets`

  * [!UICONTROL Metric]: `New Tickets`

* Metric `A`: `New tickets`
* Metric `B`: `Solved tickets`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Chart Type`: `Line`

* **[!UICONTROL Time to first response]**
  * [!UICONTROL Metric]: `Average time to first response`

* Metric `A`: `Average time to first response`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Chart Type`: `Column`

* **[!UICONTROL Time to resolution]**
  * [!UICONTROL Metric]: `Average time to resolution`
  * [!UICONTROL Filter]:
  * status IN `solved, closed`

* Metric `A`: `Average time to resolution`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Chart Type`: `Column`

* **[!UICONTROL Distinct users filing tickets]**
  * [!UICONTROL Metric]: `Distinct users filing tickets`

* Metric `A`: `Distinct users filing tickets`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Chart Type`: `Column`

* **[!UICONTROL Peak ticket days]**
  * [!UICONTROL Metric]: `New Tickets`

* Metric `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Group by`: `Ticket created_at (day of week)`
* `Chart Type`: `Pie`

* **[!UICONTROL Peak ticket hours]**
  * [!UICONTROL Metric]:`New Tickets`

  * `Show top/bottom`: `Top 100% sorted by created_at (hour of the day)`

* Metric `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Group by`: `Ticket created_at (hour of the day)`
* `Chart Type`: `Pie`

* **[!UICONTROL Avg LTV of users who have and have not filed tickets]**
  * [!UICONTROL Metric]: `Average lifetime revenue`

* Metric `A`: `Average lifetime revenue`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Group by`: `User has filed a support ticket?`
* `Chart Type`: `Column`

* **[!UICONTROL Number of new users who have and have not filed tickets]**
  * [!UICONTROL Metric]: Users

* Metric `A`: `New users`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Group by`: `User has filed a support ticket?`
* `Chart Type`: `Column`

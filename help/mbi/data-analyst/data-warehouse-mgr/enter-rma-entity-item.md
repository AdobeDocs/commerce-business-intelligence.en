---
title: Enterprise_Rma_Item_Entity Table
description: Learn how to analyze information about a specific item from a requested return.
exl-id: aa71cb3f-3e0b-4b6b-b4cc-dad103f79c51
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
---
# enterprise_rma_item_entity Table

Each row in the `enterprise_rma_item_entity` table (often called `magento_rma_item_entity` in Commerce 2.x, but the name can be customized) contains information about a specific item from a requested return. 

>[!NOTE]
>
>This table only comes standard with your Commerce account if you are an `Enterprise Edition` or `Enterprise Cloud Edition` customer.

## Common Native Columns

|**Column Name**|**Description**|
|---|---|
|`entity_id`|Unique identifier for the table. Each `entity_id` represents an item that has been requested for return.|
|`rma_entity_id`|Foreign key associated with the `enterprise_rma` table.|
|`status`|The status of the item's return. Values include 'received', 'pending', 'authorized', among others. The values in this status may not match the value of the overall return's status.|
|`qty_requested`|The quantity the customer requests for return.|
|`qty_approved`|The quantity approved for return.|
|`qty_returned`|The quantity returned.|
|`order_item_id`|Foreign key associated with the `sales_flat_order_item` table.|
|`product_sku`|The sku being returned.|

{style="table-layout:auto"}

## Common Calculated Columns

|**Column Name**|**Description**|
|---|---|
|`Return date_requested`|This is the date that the customer requested the return.|
|`Item price`|The price of the item.|
|`Return item's total value (qty_returned * price)`|This is the total monetary value of the items that are returned. This is used to calculate the total return amount on the `enterprise_rma` table.|

{style="table-layout:auto"}

## Common Metrics

|**Metric Name**|**Description**|**Construction**|
|---|---|---|
|`Number of items returned`|The number of items that are returned.|Operation Column: qty returned<br>Operation: Sum<br>Timestamp Column: Return date requested |
|`Returned items' total value`|The monetary amount returned. |Operation Column: Return item's total value (qty returned * price)<br>Operation: Sum<br>Timestamp Column: Return date requested|

{style="table-layout:auto"}

## Connections to Other Tables

`enterprise_rma`

* Create joined columns such as `Return date_requested` on the `enterprise_rma_item_entity` table via the following join:
* Commerce 1.x: `enterprise_rma_item_entity.rma_entity_id ` (many) => `enterprise_rma.entity_id` (one)
* Commerce 2.x: `magento_rma_item_entity.rma_entity_id ` (many) => `magento_rma.entity_id` (one)

`sales_flat_order_item`

* Create joined columns on the  `enterprise_rma_item_entity` table via the following join:

* Commerce 1.x: `enterprise_rma_item_entity.order_item_id ` (many) => `sales_flat_order_item.item_id` (one)
* Commerce 2.x: `magento_rma_item_entity.order_item_id ` (many) => `sales_order_item.item_id` (one)

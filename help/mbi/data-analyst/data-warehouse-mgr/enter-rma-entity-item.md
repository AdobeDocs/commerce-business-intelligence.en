---
title: Enterprise_Rma_Item_Entity Table
description: Learn how analyze information about a specific item from a requested return.
---
# enterprise_rma_item_entity Table

Each row in the `enterprise_rma_item_entity` table (often called `magento_rma_item_entity` in Magento 2.x, but the name can be customized) contains information about a specific item from a requested return. **Note:** _This table only comes standard with your Magento account if you are an Enterprise Edition or Enterprise Cloud Edition customer._

## Common Native Columns

|**Column Name**|**Description**|
|---|---|
|entity\_id|Unique identifier for the table. Each `entity\_id` represents an item that has been requested for return.|
|rma\_entity\_id|Foreign key associated with the `enterprise\_rma` table.|
|status|The status of the item's return. Values include 'received', 'pending', 'authorized', among others. The values in this status will not necessarily match the value of the overall return's status.|
|qty\_requested|The quantity the customer requests for return.|
|qty\_approved|The quantity the approved for return.|
|qty\_returned|The quantity actually returned.|
|order\_item\_id|Foreign key associated with the `sales\_flat\_order\_item` table.|
|product\_sku|The sku being returned.|

## Common Calculated Columns

|**Column Name**|**Description**|
|---|---|
|Return date\_requested|This is the date the customer requested the return.|
|Item price|The price of the item.|
|Return item's total value (qty\_returned * price)|This is the total monetary value of the items that are returned. This will be used to calculate the total return amount on the `enterprise\_rma` table.|

## Common Metrics

|**Metric Name**|**Description**|**Construction**|
|---|---|---|
|Number of items returned|The number of items that are returned.|Operation Column: qty returned<br>Operation: Sum<br>Timestamp Column: Return date requested |
|Returned items' total value|The monetary amount returned. |Operation Column: Return item's total value (qty returned * price)<br>Operation: Sum<br>Timestamp Column: Return date requested|

## Connections to Other Tables

`enterprise_rma`

* Create joined columns such as `Return date\_requested` on the `enterprise_rma_item_entity` table via the following join:
* Magento 1.x: `enterprise_rma_item_entity.rma_entity_id ` (many) => `enterprise_rma.entity_id` (one)
* Magento 2.x: `magento_rma_item_entity.rma_entity_id ` (many) => `magento_rma.entity_id` (one)

`sales_flat_order_item`

* Create joined columns on the  `enterprise_rma_item_entity` table via the following join:

* Magento 1.x: `enterprise_rma_item_entity.order_item_id ` (many) => `sales_flat_order_item.item_id` (one)
* Magento 2.x: `magento_rma_item_entity.order_item_id ` (many) => `sales_order_item.item_id` (one)

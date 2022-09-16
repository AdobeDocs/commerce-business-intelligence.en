---
title: Enterprise_Rma Table
zendesk_id: 360016503312
---

Each row in the `enterprise_rma` table (often called `magento_rma` in Magento 2.x, but the name can be customized) contains information about a specific return request. **Note:** _This table only comes standard with your Magento account if you are an Enterprise Edition or Enterprise Cloud Edition customer._

### Common Native Columns

|**Column Name**|**Description**|
|---|---|
|entity\_id|Unique identifier for the table. Each \`entity\_id\` represents a return request.|
|date\_requested|The date that the return was requested.|
|status|The status of the return. Values include 'received', 'pending', 'authorized', among others.|
|order\_id|Foreign key associated with the \`sales\_flat\_order\` table.|
|customer\_id|Foreign key associated with the \`customer\_entity\` table.|

### Common Calculated Columns

|**Column Name**|**Description**|
|---|---|
|Order's created\_at|This is the date of the original order. This can be used to obtain the time between order and return request.|
|Customer's order number|This is the customer's order number associated with the original order.|
|Seconds between order's created\_at and return's date\_requested|The number of seconds from the order date to the return request.|
|Return's total value|This is the total monetary amount that is returned. This will be the sum of each return item's individual return amount.|

### Common Metrics

|**Metric Name**|**Description**|**Construction**|
|---|---|---|
|Number of returns|The number of returns requested.|Operation Column: entity\_id<br>Operation: Count<br>Timestamp Column: date\_requested|
|Total returned amount|The total monetary amount returned.|Operation Column: Return's total value<br>
Operation: Sum<br>Timestamp Column: date\_requested|
|Average returned amount|The average monetary amount returned.|Operation Column: Return's total value<br>Operation: Average<br>Timestamp Column: date\_requested|
|Average time to return|The average time from order to return.|Operation Column: Seconds between order's created\_at and return's date\_requested<br>Operation: Average<br>Timestamp Column: date\_requested|

### Connections to Other Tables

`sale_flat_order`

* Create joined columns to segment and filter by order-level attributes on the `enterprise_rma` table via the following join:
    * Magento 1.x: `enterprise_rma.order_id` (many) => `sales_flat_order.entity_id` (one)
    * Magento 2.x: `magento_rma.order_id` (many) => `sales_order.entity_id` (one)

`enterprise_rma_item_entity`

* Create many-to-one columns such as \`Return's total value\` on the `enterprise_rma` table via the following join:
    * Magento 1.x: `enterprise_rma_item_entity.rma_entity_id` (many) => `enterprise_rma.entity_id` (one)
    * Magento 2.x: `magento_rma_item_entity.rma_entity_id ` (many) => `magento_rma.entity_id` (one)

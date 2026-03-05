---
title: Enterprise_Rma_Item_Entity Table
description: Learn how to analyze information about a specific item from a requested return.
exl-id: aa71cb3f-3e0b-4b6b-b4cc-dad103f79c51
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/jBMtEluq3XNIzItebuvDQ43PAuW6mAsyG7RkHn8URJ4
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
---
# enterprise_rma_item_entity Table

Each row in the `enterprise_rma_item_entity` table (often called `magento_rma_item_entity` in Commerce 2.x, but the name can be customized) contains information about a specific item from a requested return. 

>[!NOTE]
>
>This table only comes standard with your Commerce account if you are an `Enterprise Edition` or `Enterprise Cloud Edition` customer.

## Common Native Columns

|**Column Name**|**Description**|
|---|---|
|`entity\_id`|Unique identifier for the table. Each `entity\_id` represents an item that has been requested for return.|
|`rma\_entity\_id`|Foreign key associated with the `enterprise\_rma` table.|
|`status`|The status of the item's return. Values include 'received', 'pending', 'authorized', among others. The values in this status may not match the value of the overall return's status.|
|`qty\_requested`|The quantity the customer requests for return.|
|`qty\_approved`|The quantity approved for return.|
|`qty\_returned`|The quantity returned.|
|`order\_item\_id`|Foreign key associated with the `sales\_flat\_order\_item` table.|
|`product\_sku`|The sku being returned.|

{style="table-layout:auto"}

## Common Calculated Columns

|**Column Name**|**Description**|
|---|---|
|`Return date\_requested`|This is the date that the customer requested the return.|
|`Item price`|The price of the item.|
|`Return item's total value (qty\_returned * price)`|This is the total monetary value of the items that are returned. This is used to calculate the total return amount on the `enterprise\_rma` table.|

{style="table-layout:auto"}

## Common Metrics

|**Metric Name**|**Description**|**Construction**|
|---|---|---|
|`Number of items returned`|The number of items that are returned.|Operation Column: qty returned<br>Operation: Sum<br>Timestamp Column: Return date requested |
|`Returned items' total value`|The monetary amount returned. |Operation Column: Return item's total value (qty returned * price)<br>Operation: Sum<br>Timestamp Column: Return date requested|

{style="table-layout:auto"}

## Connections to Other Tables

`enterprise_rma`

* Create joined columns such as `Return date\_requested` on the `enterprise_rma_item_entity` table via the following join:
* Commerce 1.x: `enterprise_rma_item_entity.rma_entity_id ` (many) => `enterprise_rma.entity_id` (one)
* Commerce 2.x: `magento_rma_item_entity.rma_entity_id ` (many) => `magento_rma.entity_id` (one)

`sales_flat_order_item`

* Create joined columns on the  `enterprise_rma_item_entity` table via the following join:

* Commerce 1.x: `enterprise_rma_item_entity.order_item_id ` (many) => `sales_flat_order_item.item_id` (one)
* Commerce 2.x: `magento_rma_item_entity.order_item_id ` (many) => `sales_order_item.item_id` (one)

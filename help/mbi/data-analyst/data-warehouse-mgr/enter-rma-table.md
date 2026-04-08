---
title: enterprise_rma Table
description: Learn how to analyze information about a specific return request.
exl-id: a19cbc9a-e34f-4f4e-820f-9e413d1a552d
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/ofPlk5xNr8aspjFlpzEtDtjcOPm9DrQFYX9-vPDfK6w
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
# enterprise_rma Table

Each row in the `enterprise_rma` table (often called `magento_rma` in Adobe Commerce 2.x, but the name can be customized) contains information about a specific return request. 

>[!NOTE]
>
>This table only comes standard with your Adobe Commerce account if you are an `Enterprise Edition` or `Enterprise Cloud Edition` customer.

## Common Native Columns

|**Column Name**|**Description**|
|---|---|
|`entity_id`|Unique identifier for the table. Each `entity_id` represents a return request.|
|`date_requested`|The date that the return was requested.|
|`status`|The status of the return. Values include 'received', 'pending', 'authorized', among others.|
|`order_id`|Foreign key associated with the `sales_flat_order` table.|
|`customer_id`|Foreign key associated with the `customer_entity` table.|

{style="table-layout:auto"}

## Common Calculated Columns

|**Column Name**|**Description**|
|---|---|
|`Order's created_at`|This is the date of the original order. This can be used to obtain the time between order and return request.|
|`Customer's order number`|This is the customer's order number associated with the original order.|
|`Seconds between order's created_at and return's date_requested`|The number of seconds from the order date to the return request.|
|`Return's total value`|This is the total monetary amount that is returned. This is the sum of each return item's individual return amount.|

{style="table-layout:auto"}

## Common Metrics

|**Metric Name**|**Description**|**Construction**|
|---|---|---|
|`Number of returns`|The number of returns requested.|`Operation` column: `entity_id`<br>`Operation`: `Count`<br>`Timestamp` Column: `date requested`|
|`Total returned amount`|The total monetary amount returned.|`Operation `Column: `Return's total value`<br>`Operation`: Sum<br>`Timestamp` Column: date requested|
|`Average returned amount`|The average monetary amount returned.|`Operation`` Column: Return's total value`<br>`Operation`: `Average`<br>`Timestamp` Column: `date requested`|
|`Average time to return`|The average time from order to return.|`Operation` Column: Seconds between order's created at and return's date requested<br>`Operation`: `Average`<br>`Timestamp` Column: `date requested`|

{style="table-layout:auto"}

## Connections to Other Tables

`sale_flat_order`

* Create joined columns to segment and filter by order-level attributes on the `enterprise_rma` table via the following join:
    * Commerce 1.x: `enterprise_rma.order_id` (many) => `sales_flat_order.entity_id` (one)
    * Commerce 2.x: `magento_rma.order_id` (many) => `sales_order.entity_id` (one)

`enterprise_rma_item_entity`

* Create many-to-one columns such as `Return's total value` on the `enterprise_rma` table via the following join:
    * Commerce 1.x: `enterprise_rma_item_entity.rma_entity_id` (many) => `enterprise_rma.entity_id` (one)
    * Commerce 2.x: `magento_rma_item_entity.rma_entity_id ` (many) => `magento_rma.entity_id` (one)

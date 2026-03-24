---
title: Repeat Order Probability Report
description: Learn and understand the Repeat Order Probability Report.
exl-id: 2c88b85a-7320-44ca-87a5-5b91250348ea
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
TQID: https://experienceleague.adobe.com/MW9jxiwitZyjc6-woelN-FOAmvEFPCWDt01wyTOX16k
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
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
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
---
# Repeat Order Probability Report

## When is the `Incremental Event Probability` perspective available?

The `incremental event probability` perspective is only available when filters use dimensions that are equal for all orders (for example, user's `gender`, user's `age` or user's `source`).

This is because this perspective relies on a dimension called `User's order number` for segmentation, which numbers a user's purchases (for example, John's 1st, 2nd, and 3rd orders).

If you added a filter that uses a dimension which is not equal for all orders (for example, `Order's Region`), the `User's order number` dimension would no longer be accurate. This is because it does not account for specific regions when numbering a user's orders (for example, John's 1st, 2nd, 3rd orders are still the same, regardless of their region).

## Turning an order-specific dimension into a user-specific dimension

In certain cases, you may be able to turn an `order-specific` dimension into a `user-specific` dimension to add as filter in the `Repeat Order Probability` chart. In these cases, you return the order attribute of a user's first order or latest order (for example, User's first order region name).

If you want to create such a new dimension, [contact support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

## Comparing repeat probability of orders with different attributes

To compare the number of repeat purchases for different order attributes (for example, order's `region`), Adobe recommends creating a chart similar to `Users by lifetime number of orders`. This shows you the number of users that made 1, 2, 3,... lifetime number of orders, and add the order level filter. (in other words, This can show you whether users make more or less repeat purchases in one region or another.)

The numbers that make up such a chart can then be exported to excel to calculate the repeat order probability ratio. To see the probability of customers that made `(x)` orders to make `(x+1)` orders, simply` divide the number of people who've made at least (x+1) purchases by the number of people who have made at least (x)` purchases.

### Example:

|Category |Value |
|---|---|
|Number of customers who made 1 purchase in their lifetime|`90`|
|Number of customers who made 2 purchases in their lifetime|`30`|
|Number of customers who made 3 purchases in their lifetime|`10`|
|The repeat order probability of customers who've made one purchase in their lifetime to make a second purchase|`(30 + 10) / (30+10+90) = 30.77%`|

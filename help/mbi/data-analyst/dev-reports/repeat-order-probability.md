---
title: Repeat Order Probability Report
description: Learn and understand the Repeat Order Probability Report.
exl-id: 2c88b85a-7320-44ca-87a5-5b91250348ea
---
# Repeat Order Probability Report

## When is the `Incremental Event Probability` perspective available?

The `incremental event probability` perspective is only available when filters use dimensions that are equal for all orders (for example, user's `gender`, user's `age` or user's `source`)

This is because this perspective relies on a dimension called `User's order number` for segmentation, which numbers a user's purchases (for example, John's 1st, 2nd, and 3rd orders).

If you added a filter that uses a dimension which is not equal for all orders (for example, `Order's Region`), the `User's order number` dimension would no longer be accurate. This is because it does not account for specific regions when numbering a user's orders (for example, John's 1st, 2nd, 3rd orders are still the same, regardless of their region).

## Turning an order-specific dimension into a user-specific dimension

In certain cases, you may be able to turn an `order-specific` dimension into a `user-specific` dimension to add as filter in the `Repeat Order Probability` chart. In these cases, you return the order attribute of a user's first order or latest order (for example, User's first order region name).

If you want to create such a new dimension, [contact support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).

## Comparing repeat probability of orders with different attributes

To compare the number of repeat purchases for different order attributes (for example, order's `region`), Adobe recommends creating a chart similar to `Users by lifetime number of orders`. This shows you the number of users that made 1, 2, 3,... lifetime number of orders, and add the order level filter. (in other words, This can show you whether users make more or less repeat purchases in one region or another.)

The numbers that make up such a chart can then be exported to excel to calculate the repeat order probability ratio. To see the probability of customers that made `(x)` orders to make `(x+1)` orders, simply` divide the number of people who've made at least (x+1) purchases by the number of people who have made at least (x)` purchases.

### Example:

| | |
|---|---|
|Number of customers who made 1 purchase in their lifetime|`90`|
|Number of customers who made 2 purchases in their lifetime|`30`|
|Number of customers who made 3 purchases in their lifetime|`10`|
|The repeat order probability of customers who've made one purchase in their lifetime to make a second purchase|`(30 + 10) / (30+10+90) = 30.77%`|

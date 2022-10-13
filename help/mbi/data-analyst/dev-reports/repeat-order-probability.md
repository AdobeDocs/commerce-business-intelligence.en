---
title: Repeat Order Probability Report
description: Learn and understand the Repeat Order Probability Report.
---
# Repeat Order Probability Report

## When is the Incremental Event Probability perspective available?

The incremental event probability perspective is only available when filters use dimensions that are equal for all orders (e.g., user's gender, user's age, user's source, etc.)

This is because this perspective relies on a dimension called "User's order number" for segmentation, which numbers a user's purchases (e.g., John's 1st, 2nd, 3rd orders, etc.).

If we were to add a filter that uses a dimension which is not equal for all orders (e.g., "Order's Region"), the "User's order number" dimension would no longer be accurate as it does not account for specific regions when numbering a user's orders (i.e., John's 1st, 2nd, 3rd orders are still the same, regardless of their region).

## Turning an order-specific dimension into a user-specific dimension

In certain cases, we may be able to turn an order-specific dimension into a user-specific dimension to add as filter in the Repeat Order Probability chart. In these cases, we will return the order attribute of a user's first order or latest order (e.g., User's first order region name).

If you want to create such a new dimension, [contact support](../../getting-started/support.md).

## Comparing repeat probability of orders with different attributes

To compare the number of repeat purchases for different order attributes (e.g., order's region), we recommend creating a chart similar to "Users by lifetime number of orders" which shows you the number of users that made 1, 2, 3,... lifetime number of orders, and add the order level filter. (e.g., This can show you whether users make more or less repeat purchases in one region or another.)

The numbers that make up such a chart can then be exported to excel to calculate the repeat order probability ratio. To see the probability of customers that made (x) orders to make (x+1) orders, simply **divide the number of people who've made at least (x+1) purchases by the number of people who have made at least (x)** purchases.

### Example:

| | |
|---|---|
|Number of customers who made 1 purchase in their lifetime|`90`|
|Number of customers who made 2 purchases in their lifetime|`30`|
|Number of customers who made 3 purchases in their lifetime|`10`|
|The repeat order probability of customers who've made one purchase in their lifetime to make a second purchase|`(30 + 10) / (30+10+90) = 30.77%`|

---
title: Analyzing Customer Repurchasing Behavior
description: Learn how to analyze customer repurchase behavior.
exl-id: 62666d08-5240-4f19-bf8e-e5b2d79a25c4
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards
TQID: https://experienceleague.adobe.com/AM-l7yCwm00r5uqmqD-z34GN3rubycbTnWeTQ4oHI8k
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
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
---
# Customer Repurchasing Behavior

If you offer more than one product, you probably wonder how customers that purchase a specific product behave differently over time compared to other customers. This topic explores analyses that can help you answer the following questions.

Among customers who purchase a *specific item*,

* What is the probability that they make another purchase?
* How long does it take for them to make another purchase?
* What is the average number of orders customers place in the short/long term?
* What is the average revenue customers generate in the short/long term?

## Recommended metrics

When building customer repurchasing activity analyses, Adobe recommends using the following metrics:

### Repeat order probability

This measure is defined as the total number of repeat orders, as a percent of total orders. In other words, this is the likelihood that an order is followed by another order. This measure identifies items that are likely to entice customers to come back to your store.

### Average number of orders placed

This exposes your customers' purchasing behavior, specifically how many orders your customers have placed over a given time period. You can choose to limit this measure to see customers' behavior in the short, medium, or long term. Some products may encourage customers to make frequent purchases in the shorter term, while others may influence a customer's long-term loyalty. If this number is higher for one item compared to other items, this would suggest that people who buy this item are the ones that come back to your store.

### Average customer lifetime revenue

This metric allows you to understand whether customers who purchase specific items are more valuable over the course of their lifetime. If this number is higher for one item compared to other similarly priced items, this would suggest that your higher-value customers tend to purchase this item.

### Time to next order

This measure shows customer's ordering frequency, or the time it takes for the customer to order again. If the time to next order is shorter for one item compared to other items, this would suggest that people who purchase this item tend to come back sooner.

## Today's example: coffee products

Keeping the above metrics in mind, look at an example involving coffee products.

| **Product name** | **Repeat order probability** | **Avg lifetime number of orders** | **Avg lifetime revenue** | **Median time to next order** |
|-----|-----|-----|-----|-----|
| Single-cup coffee brewer | 94.98% | 7.92 | $549.82 | 57.01 days |
| Coffee capsules | 93.82% | 8.68 | $479.98 | 63.48 days |
| Coffee beans | 41.92% | 6.07 | $99.82 | 27.31 days |

{style="table-layout:auto"}

Now that you have your data, what does this mean for each of your metrics?

### Repeat order probability

In this example, the repeat order probability - or the likelihood that an order is followed by another order - is much higher for the single-cup coffee brewers and coffee capsules than for the coffee beans.

Since customers who purchase the brewer are "committed" to purchasing the associated capsules going forward, this makes sense. Similarly, the customers who purchased capsules have a brewer that is compatible with the capsules. However, coffee beans are not specific to any particular brewer.

### Average lifetime number of orders

Based on the data above, you can see that people who purchase the brewer or capsules have made more purchases in their lifetime, on average, compared to customers who have purchased coffee beans.

### Average customer lifetime revenue

Customers who purchase the brewer have the highest average lifetime revenue, which makes sense, given that the cost of the brewer is included in this measure. In contrast, customers who purchase coffee beans typically only purchase low-cost items.

### Time to next order

Among customers who have purchased coffee capsules, half make a repeat order in about two months. However, among customers who have purchased coffee beans, half make a repeat order in about one month. This could be because people who order capsules either (1) do not drink as much coffee, or (2) place orders in bulk (for example, purchasing two months' worth of coffee in one order).

## What other analyses can I build?

Using the metrics outlined in this topic, you can also build other useful repurchasing analyses. For example, you can also see how customers repurchase **the same item** - for example, if they buy refills regularly. Capsules and coffee beans may be repurchased regularly, but it would be unexpected to see customers making repeat purchases of the coffee brewer. If your business focuses on refills or restocking, this analysis would be useful.

In addition to analyzing the repurchasing behavior of your customers, you can also build analyses that look at customer loyalty. Consider analyzing patterns in customer churn - where are your customers leaving your site and not coming back? At what rate is this occurring?

Once you have identified why churn is happening, you can use your analysis to build a `reactivation` campaign. Using this data, you can identify users who've become inactive, how long it has been since their last visit, what their last purchase was, and so on. This allows you to make actionable decisions that entice your customers to come back.

For help with analysis, [contact support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

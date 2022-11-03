---
title: Analyzing Customer Repurchasing Behavior
description: Learn how to analyze customer repurchase behavior. 
---
# Customer Repurchasing Behavior

If you offer more than one product, you probably wonder how customers that purchase a specific product behave differently over time compared to other customers. In this article, we explore analyses that can help you answer the following questions:

Among customers who purchase a *specific item*,

* What is the probability they will make another purchase?
* How long will it take for them to make another purchase?
* What is the average number of orders customers place in the short/long term?
* What is the average revenue customers generate in the short/long term?

## Recommended metrics

When building customer repurchasing activity analyses, we recommend using the following metrics:

### Repeat order probability

This measure is defined as the total number of repeat orders, as a percent of total orders. In other words, this is the likelihood that an order will be followed up by another order. This measure identifies items that are likely to entice customers to come back to your store.

### Average number of orders placed

This exposes your customers' purchasing behavior, specifically how many orders your customers have placed over a given time period. You can choose to limit this measure to see customers' behavior in the short, medium, or long term. Some products may encourage customers to make frequent purchases in the shorter term, while others may influence a customer's long term loyalty. If this number is higher for one item compared to other items, this would suggest that people who buy this item are the ones that come back to your store.

### Average customer lifetime revenue

This metric allows you to understand whether customers who purchase specific items are more valuable over the course of the their lifetime. If this number is higher for one item compared to other similarly-priced items, this would suggest that your higher-value customers tend to purchase this item.

### Time to next order

This measure shows customer's ordering frequency, or the time it takes for the customer to order again. If the time to next order is shorter for one item compared to other items, this would suggest that people who purchase this item tend to come back sooner.

## Today's example: coffee products

Keeping the above metrics in mind, Let us take a look at an example involving coffee products.

| **Product name** | **Repeat order probability** | **Avg lifetime number of orders** | **Avg lifetime revenue** | **Median time to next order** |
|-----|-----|-----|-----|-----|
| Single-cup coffee brewer | 94.98% | 7.92 | $549.82 | 57.01 days |
| Coffee capsules | 93.82% | 8.68 | $479.98 | 63.48 days |
| Coffee beans | 41.92% | 6.07 | $99.82 | 27.31 days |

{style="table-layout:auto"}

Now that we have our data, lets take a look at what this could mean for each of our metrics.

### Repeat order probability

In this example, the repeat order probability - or the likelihood that an order will be followed up by another order - is much higher for the single-cup coffee brewers and coffee capsules than for the coffee beans.

Since customers who purchase the brewer are "committed" to purchasing the associated capsules going forward, this makes sense. Similarly, the customers who purchased capsules have a brewer that is compatible with the capsules. However, coffee beans are not specific to any particular brewer.

### Average lifetime number of orders

Based on the data above, we can see that people who purchase the brewer or capsules have made more purchases in their lifetime, on average, compared to customers who have purchased coffee beans.

### Average customer lifetime revenue

Customers who purchase the brewer have the highest average lifetime revenue; which makes sense, given that the cost of the brewer is included in this measure. In contrast, customers who purchase coffee beans typically only purchase low-cost items.

### Time to next order

Among customers who have purchased coffee capsules, half make a repeat order in about 2 months. However, among customers who have purchased coffee beans, half make a repeat order in about 1 month. This could be because people who order capsules either (1) do not drink as much coffee, or (2) place orders in bulk (for example, purchasing 2 months' worth of coffee in one order).

## What other analyses can I build?

Using the metrics we outlined in this article, you can also build other useful repurchasing analyses. For example, we can also see how customers repurchase **the same item** - for example, if they buy refills on a regular basis. Capsules and coffee beans may be repurchased regularly, but it would be unexpected to see customers making repeat purchases of the coffee brewer. If your business focuses on refills or restocking, this analysis would be extremely useful.

In addition to analyzing the repurchasing behavior of your customers, you can also build analyses that look at customer loyalty. Consider analyzing patterns in customer churn - where are your customers leaving your site and not coming back? At what rate is this occurring?

Once you have identified why churn is happening, you can use your analysis to build a `reactivation` campaign. Using this data, you can identify users who've become inactive, how long it is been since their last visit, what their last purchase was, and so on. This will allow you to make actionable decisions that will entice your customers to come back.

For help with analysis, [contact support](../../getting-started/support.md).

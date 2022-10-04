---
title: Analyzing coupon impact
description: Learn how to analyzing coupon impact on acquiring and retaining customers. 
---
# Coupon Impact

Analyzing how customers use your coupons can provide significant insight into your business. Specifically, analyzing how you acquire and retain customers via coupons. In this article, we explore analyses that can help you answer the following types of questions:

* How many customers are you acquiring via coupons?
* Are coupon-acquired customers more likely to make repeat purchases than customers not acquired through coupons?
* How does average lifetime revenue differ between coupon-acquired customers and customers not acquired through coupons?
* Do customers acquired from coupons make repeat purchases with coupons?

To answer these questions, we focus on [comparing coupon-acquired customers to non-coupon acquired customers](../#compare), [analyzing first order details from coupon acquisitions](../#firstorder), and [looking at the attributes of customers who use coupons in their first order.](../#attributes)

Let us get started!

## Comparing coupon-acquired customers to non-coupon acquired customers {#compare}

When building analyses that explore your coupon acquisition and retention, consider using the following metrics:

### Number of new customers

This metric shows you the number of coupon-acquired customers and non-coupon acquired customers over all time. This can help you determine the ratio of customer acquisitions via coupons.

### Average lifetime revenue

This metric shows you the average lifetime revenue from coupon and non-coupon acquired customers. This can help determine if the lifetime value of a customer varies depending on their acquisition type.

### Number of repeat orders

This metric shows you the number of repeat orders made by both types of customer acquisitions. This can help determine if more follow-up orders are placed by coupon acquired or non-coupon acquired customers.

### Number and percent of repeat orders with coupon

This shows the number of repeat orders made with a coupon applied and the percent of repeat orders made with a coupon. This can help you determine if coupon-acquired customers tend to make more repeat orders with a coupon than non-coupon acquired customers and if coupon-acquired customers are disproportionately using coupons in their follow up orders.

Let us look at some sample data for coupon acquisition versus non-coupon acquisition metrics:

| **Customer acquisition** | **Number of new customers** | **Average lifetime revenue** | **Number of repeat orders** | **Number of repeat orders w/ coupon** | **% of repeat orders w/ coupon** |
|-----|-----|-----|-----|-----|-----|
| Coupon | 1,206 | $356.91 | 2,570 | 1,248 | 48.56% |
| Non-coupon | 11,561 | $498.30 | 20,145 | 3,251 | 16.14% |

{style="table-layout:auto"}

What can we take away from this? Let us take a look:

### Number of new customers

In the above example, there is a much larger number of non-coupon acquisitions than coupon acquisitions. However, there are still 1,206 customers acquired via a coupon that may otherwise not have become customers.

### Average lifetime revenue

In this example, non-coupon acquisitions have a higher average lifetime revenue than coupon acquisitions. This implies that non-coupon acquisitions are making more repeat purchases and/or are making higher value purchases.

### Number of repeat orders

The number of repeat orders for non-coupon acquisitions is much higher than coupon acquisitions. This is expected because there are many more non-coupon acquired customers.

### Number of repeat orders with coupon

Similarly, the number of repeat orders made with a coupon are higher for non-coupon acquisitions.

## #Percent of repeat orders with coupon

Non-coupon acquired customers have a much lower percent of repeat orders with a coupon applied than coupon acquired customers. Thus, for coupon-acquired customers, almost one out of every two repeat orders has a coupon applied. In this example, coupon acquired customers tend to make repeat purchases with coupons.

## Analyzing first order details from coupon acquisitions {#firstorder}

In this section, we focus only on **first orders from coupon acquisitions, segmented by coupon.** we use these metrics in our analysis:

### Number of orders/customers

This metric shows you the number of first time orders for each coupon, or the number of customers who used that coupon in their first order. This can help determine if a certain coupon encourages more first time purchases than other coupons.

### Gross revenue

This metric reveals the revenue you earn from a particular coupon that was used in a customer's first order. This revenue is a calculation of items sold before any discounts are applied.

### Discounts from coupons

This metric shows you the total discount amount applied from the coupons.

### Net revenue

This metric reveals the revenue you earn from a particular coupon that was used in a customer's first order. This revenue is a calculation of items sold after all discounts are applied. it is important to note that the net revenue may not have occurred without the coupons.

### Average order value

This metric reveals the average order value for a particular coupon.

### Average lifetime number of orders

This metric helps evaluate the loyalty and average number of orders generated by customers who use a certain coupon.

### Average lifetime revenue

This metric helps evaluate the loyalty and average revenue generated by customers who use a certain coupon. When evaluating whether customers who use coupons are higher value than others, be sure to take into account the number of orders each coupon was used in to ensure that you have a significant sample size.

Now, Let us look at an example involving three different coupons used for customers' first time order:

| **Coupon** | **First time orders (FTO)** | **Gross revenue from FTO** | **Discounts applied to FTO** | **Net revenue from FTO** | **Average order value for FTO** |
|-----|-----|-----|-----|-----|-----|
| **25% off $100 or more** | 56 | $8,531.04 | $2,132.76 | $6,398.28 | $152.34 |
| **$10 off** | 87 | $3,707.07 | $426.10 | $3,280.97 | $42.61 |
| **20% off** | 145 | $10,975.05 | $2,195.01 | $8,780.04 | $75.69 |

{style="table-layout:auto"}

What can we take away from this? First, the "20% off" coupon had the most number of first time orders. However, the number of orders associated with each coupon could vary based on several factors, including:

* the amount of advertisement for each coupon.
* the length of time for which the coupons were offered.
* the time of day/week/month/year the coupons were offered.
* the season the coupons were offered, depending on the business.

  **Example:** the "20% off" coupon was offered during the summer months, but the business sells winter clothing.
* the restrictions on the coupons.

  **Example:** the "10% off" coupon is only offered to customers who purchase a winter coat in the same order.

The **gross revenue** for the "25% off $100 or more" coupon is much higher than the gross revenue for the "$10 off" coupon. However, the "$10 off" coupon has a much larger **number of orders**. Analyzing the **average order value** provides insight into these differences: even though the "25% off $100 or more" coupon had fewer number of orders, the average order value is over triple that of the "$10 off" coupon. Thus, a larger gross revenue is attributed to the "25% off $100 or more" coupon.

The **discounts** and **net revenue** for the "25% off $100 or more" and "20% off" coupons are close in value. Even though the average order value for "25% off $100 or more" is close to twice the average order value for "20% off", the latter coupon has a little less than triple the number of orders.

## Attributes of customers who use coupons in their first order {#attributes}

Now that we have looked at the orders themselves, Let us take a look at the customers who use coupons in their first orders:

| **Customer's first order coupon** | **Number of customers** | **Average lifetime number of orders** | **Average lifetime revenue** |
|-----|-----|-----|-----|
| **25% off $100 or more** | 56 | 2.8 | $554.54 |
| **$10 off** | 87 | 1.9 | $115.50 |
| **20% off** | 145 | 1.3 | $103.75 |

{style="table-layout:auto"}

you will notice that the number of first time orders is the same as the number of customers for each coupon. This makes sense because each customer can only have one first order.

The largest number of customers were acquired through the "20% off" coupon. However, these customers have the lowest **average lifetime number of orders** and **average lifetime revenue**; generally, most coupon-acquired customers do not make any repeat orders. Furthermore, customers acquired through the "25% off $100 or more" coupon drive higher **average lifetime number of orders** and in turn, higher **average lifetime revenue**. Generally, users who were acquired via this coupon usually come back and make more repeat purchases.

## Wrapping Up {#wrapup}

There are a multitude of analyses you can create to better understand how your customers use coupons. Ever thought about analyzing how your customers use your coupons or the time it takes for coupons to be used? What about finding the optimal discount amount - what amount encourages repeat buyers, higher average order value, and higher lifetime revenue? For help with these types of questions, [contact support](../../getting-started/support.md).

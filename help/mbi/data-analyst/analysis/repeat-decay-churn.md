---
title: Analyzing Repeat Probability Decay and Churn
description: Learn and understand how time lapses between orders and when customers are expected to churn.
exl-id: ea26052d-ac74-43b7-a4a6-977800d4c719
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Reports, Dashboards
---
# Repeat Probability Decay and Churn

If a portion of your revenue comes from repeat purchases, you are probably aware of the tremendous value of a loyal customer base. To this end, it is critical to understand how time lapses between orders and when customers are expected to churn.

This topic explores the analyses that can help you answer the following questions:

* What is the probability that a customer makes another purchase?
* How does the repeat order probability vary with time since the customer's most recent purchase?
* When should a customer be considered churned? And therefore, when should a reactivation campaign kick-off?

## Recommended metrics

When analyzing repeat probability decay and churn, consider using ([or building](../../data-user/reports/ess-manage-data-metrics.md)) these metrics:

### Initial repeat order probability

This measure is defined as the total number of repeat orders, as a percent of total orders. Phrased another way, this is the likelihood of an order to be followed up by another order. When this probability is above 50 percent, it implies that more than half of all orders are followed up by a subsequent order.

### Repeat order probability given months since order

This measure demonstrates the probability of a user ordering again given the number of months that have elapsed since their last order. The formula used to generate this metric simplifies to:

![Repeat probability formula](../../assets/Repeat_probability_formula.png)

Depending on your business model, the repeat order probability may either drop off immediately after a customer places an order and continue to decrease in subsequent months or it may demonstrate seasonal variations and spikes.

Understanding the percentage of customers that are expected to make repeat purchases (and how this trends over time) allows you to target your customers at intervals to maximize the probability of a repeat purchase. Thus, when the repeat purchase probability is decreasing, you can choose a time to identify a customer as churned and switch your efforts from retention to reactivation.

## Today's example

Look at the repeat probability decay for a typical ecommerce business.

![Initial repeat order probability repeat order probability given months since order.](../../assets/Order_probability_reports.png)

### Initial repeat order probability

In this example, the initial repeat order probability - or the likelihood that a customer makes a repeat purchase - is 60 percent. This means that 60 percent of all orders placed with this business are followed by a subsequent order.

### Repeat order probability given months since order

This report shows the probability of a customer ordering again given that some months have elapsed since their last order. Although there is no singular definition for the churn threshold given this report, Adobe recommends defining churn as the point where the probability decay crosses the value that is half of the initial repeat probability rate.

Since the initial repeat probability rate for this example is 60%, the churn date would be the time when the repeat order probability drops below 60%/2 = 30%, or at about 6 months. Out of the 60% of orders that expected to be followed with another order, half of them were placed within the first 6 months.

Phrased another way, if a customer was going to place a follow-up order, they're more likely to have done so within six months of their last order than after the six-month mark. If a customer has not repurchased after six months, a reactivation campaign should be kicked off to draw this customer back in.

Depending on your business model, you may want to instead choose a different threshold, like the point where the repeat order probability dips below 50% or 10%. If your internal knowledge suggests a different number, then by all means, you should use it!

Ultimately, the goal is to select the threshold where it makes sense to switch from retention to reactivation efforts. Retention efforts may involve emails to re-engage with existing customers with suggested follow-up purchases to make, whereas reactivation efforts may involve emails to lapsed customers with coupons and deals.

## What questions should I consider?

To help you understand repeat order probability as it applies to your business, Adobe suggests considering these questions when you explore your own data:

* Is the initial repeat order probability expected? If not, why do you think it should be higher or lower?
* Are there any large decreases in repeat order probability for specific months since last order? If so, are these changes expected?
* What is your current churn threshold?
* Does your current churn threshold align with one of the values in your Repeat order probability given months since last order report?
* Does your current threshold reflect your advertising efforts switching from retention to reactivation?
* Does it make sense for your business to change the threshold to the month where the probability decay crosses the value that is half the initial repeat probability rate?

## What else should I analyze?

After creating the above analysis and determining a churn threshold, you can build more analyses to identify common trends in churned users. For example, are customers who have churned acquired during the same time period, or did they purchase similar products in their last order? Once a churn threshold is set, you can further dive into specific traits of these churned customers.

If you offer more than one product, you probably wonder how customers that purchase a specific product behave differently over time compared to other customers. Want to know more? Check out this tutorial to explore the lifetime purchasing behavior of customer cohorts based on specific products that they have purchased.

This best practice is provided by [!DNL Adobe Commerce Intelligence] Data Analysis Services (DAS). [Contact support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) for more info.

### Related

* [Analyzing coupon impact on acquiring and retaining customers](../analysis/coupon-impact.md)
* [Analyzing customer repurchasing behavior](../analysis/repurchase-behavior.md)

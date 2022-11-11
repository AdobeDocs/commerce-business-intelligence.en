---
title: Formulas in the Report Builder
description: Learn how formulas can be used in the Report Builder.
exl-id: 7a0ad07a-5bcc-474f-95bc-ccc2b74073b2
---
# Formulas in the `Report Builder`

In the [`Report Builder`](../../tutorials/using-visual-report-builder.md), you can create powerful visualizations using the [defined metrics](../../data-user/reports/ess-manage-data-metrics.md) in your account. Combining these metrics in a formula allows you to glean additional insights from your data. In this article, we deep-dive into how formulas can be used in the `Report Builder` - lets jump in!

## What is a `formula`? {#what}

In the `Report Builder`, a `formula` is just a combination of one or more metrics based on some mathematical logic. A typical example looks like this:

![](../../assets/formula-example.png)

In this example, we are using a `Number of orders metric (A)` and a `Distinct buyers metric (B)`, and our goal is to answer the question: what is the average number of orders my buyers are making each month? The parameters of the formula are:

* `Definition`: Here, you apply math on the input metrics. In this example, dividing the number of orders by the number of distinct buyers will tell us the average number of orders. Therefore, the definition is (A/B).

* `Format`: Is your formula returning a number, a time period, or a currency amount? Next to the formula's definition is a dropdown, which you can use to specify the return's format. In this case, it is a number.

* `Miscellaneous`: The formula's timestamp, groupings, perspectives, and filters are all inherited by its input metrics. There is nothing to do here!

## How can I use `formulas` in my reports? {#how}

Now that we have covered the basics, lets take a look at some examples.

### Example: I want to find out what percent of my revenue can be attributed to first-time orders.

![Using formulas to find the percent of revenue attributed to first-time orders](../../assets/first_time_orders.gif)

In this example, we used the `Revenue` and `Revenue (first time orders)` metrics. By dividing the `Revenue (first time orders)(B)` metric by the `Revenue metric (A)` and setting the return format to `Percent`, we can find the percent of revenue that can be attributed to first time orders.

### Example: I want to know what the average revenue per order is when I do and do not offer a `promo code`.

![Using formulas to find the average revenue per order with and without promo codes](../../assets/promo_code.gif)

In this example, we used the `Revenue` and `Number of orders` metrics. The answer to this question involves two steps - dividing `Revenue (A)` by the `Number of orders (B)` and setting the return format to `Currency`. Next, we only allowed the formula result (`Avg. Revenue per order`) to show and grouped the results by `Promo code`.

### Example: I want to know the distribution of my new customers' UTM sources.

![Using formulas to find the distribution of new customers' UTM sources](../../assets/distro.gif)

Finding the answer this question involves a few steps:

1. First we added the `New Customers` metric, and then grouped by `utm_source - all`. This is metric `A`, or `New Customers (grouped)`.

1. Next, we duplicated the `New Customers (grouped)` metric and set it to use an independent dimension. Metric `B` - `New customers (ungrouped)` - shows the total number of new customers.

1. After hiding both metrics, we set the formula definition to `A/B`. This divides the `New customers (grouped)` by the `New Customers (ungrouped)`.

1. Next, we set the results format to `Percent`.

In our example, we used the `Stacked Columns` perspective to display the results by month. This allows us to compare the distribution of new customers on a month-to-month basis.

## Wrapping up {#wrapup}

Did you notice in the examples above that the formula's `timestamp`, `groupings`, `perspectives`, and `filters` are inherited from its input metrics? Keep in mind that formulas can be leveraged to use `perspectives` and [independent time options](../../tutorials/time-options-visual-rpt-bldr.md){: target="_blank"}, just like metrics can.

If you have any additional questions about using formulas in the `Report Builder`, [contact support](../../guide-overview.md).

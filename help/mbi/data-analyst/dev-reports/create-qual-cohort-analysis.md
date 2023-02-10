---
title: Create a qualitative cohort analysis
description: Learn what a qualitative cohort is, why you might be interested in building this analysis, and how you can create it in [!DNL MBI].
exl-id: 113244e4-409b-4129-b3d4-7a3433539ade
---
# Create a `Qualitative Cohort Analysis`

Do you know how your [!DNL Adwords]-acquired customer segments grow their LTV compared to those customers acquired from organic search? Have you ever thought of performing a `cohort` analysis on different customer segments side-by-side in the same report? If so, a `qualitative cohort analysis` will help you answer those questions.

In this article, we dive into what a qualitative cohort is, why you might be interested in building this analysis, and how you can create it in [!DNL MBI].

## What are `qualitative cohorts`, anyway? {#whatare}

`Cohort` analysis in general can be broadly defined as the analysis of user groups that share similar characteristics over their life cycles. It allows you to identify behavioral trends across different user groups.

See [cohort analysis](https://www.cohortanalysis.com/) - we wrote the site on it!

Most `cohort` analyses in [!DNL MBI] group users together by a common date (for example, the set of all customers who made their first purchase in a given month). A `qualitative cohort` is a little different: it is a user group that is defined by a characteristic that is not time-based. Some examples include:

* The set of all users that were acquired from an ad campaign
* The set of all users whose first purchase included a coupon (or did not)
* The set of all users who are of a certain age

## How does that differ from the normal `cohort` builder? {#different}

The [`Cohort Analysis Builder`](../dev-reports/cohort-rpt-bldr.md) is optimized for grouping cohorts using a time-based characteristic. This is great for analyses focusing on a specific segment of user (for example, all users who were acquired via a paid search campaign). In the `Cohort Analysis Builder`, you can (1) focus in on that specific user group, and (2) `cohort` on a date (like their first order date).

However, if you want to analyze the cohort behavior of multiple user segments in the same cohort report (`paid` search versus `organic` search vs direct traffic, perhaps?), this more advanced analysis can be constructed in the `Report Builder`.

## What information should I send to support to set up my analysis? {#support}

Creating a `qualitative cohort` report in the `Report Builder` involves our analyst team creating some [advanced calculated columns](../data-warehouse-mgr/creating-calculated-columns.md) on the necessary tables.

To build these, submit a [support ticket](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) (and reference this article!). Here is what we need to know:

* The `metric` you want to perform your cohort analysis with and what table it uses (example: `Revenue`, built on the `orders` table).

* The `user segments` you want to define and where that information lives in your database (example: different values of `User's referral source`, native to the `users` table and relocated down to the `orders`).

* The `cohort date` you want your analysis to use (example: the `User's first order date` timestamp). This example would allow us to look at each segment and ask `How does a user's revenue grow in the months following their first order date?`.

* The `time interval` that you want to see the analysis over (example: `weeks`, `months`, or `quarters` after the `User's first order date`).

Once our analyst team responds to the above, you will have a couple of new advanced calculated columns to build out your report! Then you will be able to follow the below directions to do this.

## Creating the qualitative cohort analysis {#create}

First, you want to add the metric you are interested in cohorting, once for each `cohort` you are analyzing. In this example, we want to see cumulative `Revenue` made in the months after a customer's first order, segmented by the `User's referral source`. This means that, for each segment, we will add one `Revenue` metric and filter for the specific segment:

![](../../assets/qualcohort1.gif)

Second, you should make two changes to the time options of the report:

1. Set the `time interval` to `None`. This is because we eventually group by the time interval as a dimension instead of using the usual time options.

1. Set the `time range` to the window of time you want the report to cover.

In our example, we look at an `all time` view of `Revenue`. After this, you should end up with a series of dots:

![](../../assets/qualcohort2.gif)

Third, you will make an adjustment to actually set up the `cohorts`. Based on the `cohort date` and `time interval` you specified to our analyst team, you will have a dimension in your account that will perform the `cohort` dating. In this example, that custom dimension is called `Months between this order and customer's first order date`. Using this dimension, you should:

* `Group by` the dimension with the `group by` option

* Select all values of the `dimension` in which you are interested

* With the `Show top/bottom option`, select the top X months that you are interested in, and sort by the `Months between this order and customer's first order date` dimension

Now, you can able to see one line for each `cohort` that you specified. Check out our example now -- we see the `Revenue` contributed by users of each referral source, `grouped by` the number of months between their first order and any subsequent order. We also added a `Cumulative perspective` to see the `cohorts'` aggregate growth - take a look at the results table for more granularity.

What does this tell us? Here, the specific referral source `Paid search` is very valuable in the first month of a customer's purchasing lifetime, but fails to retain its customer base with repeat revenue. While `Direct Traffic` starts off at a lower amount, revenue in subsequent months actually accumulates at a similar pace.

No matter how you dice it, `cohort` analysis is a powerful tool in your analysis toolbox. This type of analysis can yield some very interesting insights about your business that traditional `time-based cohorts` may not, enabling you to make better data-driven decisions.

---
title: Lifetime Revenue Cohort Analysis
description: Explore the power of Commerce Intelligence cohort analysis.
exl-id: f2b55745-d364-4ba6-9857-ce9cee05c3ae
---
# [!DNL Lifetime Revenue Cohort] Analysis

There are numerous ways to look at your data in [!DNL Adobe Commerce Intelligence], and you know that interpretation and understanding are as important as calculation and visualization. This topic explores the power of [!DNL Commerce Intelligence] `cohort` analysis.

## What does `lifetime revenue cohort` analysis mean?

The chart below shows the cumulative spending per user for a period of time after they are acquired. `Cohorts` of users are split up by their acquisition month.

For example, the orange line above shows the average for users who were acquired in November 2011. The first data point means that in their first month, users who were acquired in November spent an average of about `$200`. The second data point means that by the end of their second month, these users had spent an average of about `$240`. Their average spending in month two was approximately `$40 (240 - 200)`. The different lines represent different cohorts of users. The green line represents the users that were acquired in December, and the blue is users that were acquired in October.

## Why is this important?

This kind of `cohort` analysis can be useful for several different purposes, but the most immediate benefit is often better customer acquisition decisions. Many companies limit their marketing spend to channels that yield profitability on a customer's first purchase. These companies pay to acquire customers through a given channel as long as their average first purchase yields more `gross margin` than it costs to acquire them.

The problem with this approach is that it often results in an under investment in growth. If your competitors are marketing based on a deeper understanding of buying behavior, they outgrow you. The `lifetime revenue cohort` analysis helps you to understand the consequences of expanding your customer acquisition spending, and it provides an easy way to convey this to the rest of your team. If future customers behave like existing customers, then acquiring customers for a higher CPA result in a predictable payback period. Depending on the cash position of the business, you can define what payback period you are comfortable with, find the relevant spot on the chart, and spend accordingly. 

Also, you can use this analysis to see if you are getting better at onboarding, engaging, and generating revenue from the users you acquire. For example, this `cohort` analysis is a great way to see if a free shipping promotion for new users resulted in repeat buyers or one time purchasers that never come back.

## How will this vary for different business models?

For most businesses, the `lifetime revenue cohort` analysis chart will show a large amount of spending in the initial period and then increase more slowly over time. That initial spike is because customers are more likely to make their first purchase soon after they are acquired than at any other time. In cases where the acquisition event itself is a purchase, 100% of customers make a purchase in their first period. In cases where registration can happen before purchases, this effect is less drastic.

As an example, [!DNL Groupon] would likely have a much lower initial jump than [!DNL Amazon], because many of the people who sign up for [!DNL Groupon] do not make a purchase right away. Unless there are a high number of refunds, this chart will slope up and to the right after the initial jump. The rate of growth tends to decrease over time because customers are most active when they first sign up. This causes the average to drop because the number of people in the cohort stays constant regardless of how many come back to buy more. In subscription businesses, the slope will decay less aggressively than in businesses where people make one-time purchases.

Occasionally, a subscription business will actually have a slope that increases over time. It is rare to see this, but it is a great signal for the business when it happens. This does not mean that there are zero churning customers, but rather that upgrades for customers that stay more than make up for the customers that leave.

## How is this calculated?

There are two simple inputs to this calculation: how many members are in the `cohort` (which never changes), and how much revenue those members generated in the given period. To determine the members in the `cohort`, you count the number of users who were acquired in the period in question. An acquisition can be a first purchase, account creation, newsletter sign-up, or some other event. The `revenue` calculation is a bit more complicated. You want to sum revenue for orders that were placed by members of this `cohort` and took place within a fixed time period from their acquisition date (for example, the first three months). Finally, you divide the revenue by the number of members in the `cohort` for each time period in the chart and add this value cumulatively over time.

## What are the variations of this chart?

There are many different kinds of useful `cohort` analyses. The most common variation is [filtering by user acquisition source](../analysis/most-value-source-channel.md). For example, you might want to look at this chart for customers who came from `organic` search, `paid` search, or an affiliate program. This helps you understand if the customers from one acquisition source are more loyal or valuable than another. You can also filter by demographics or other user attributes.

Another way to look at the data is with an incremental, rather than cumulative, data perspective. This shows the incremental amount that an average user spends in each month after they are acquired. This is useful for forecasting the number of repeat purchases that you get from existing users. You can look at this with other things besides revenue as well. Some examples include margin and nonfinancial metrics like invites, votes, or messages.

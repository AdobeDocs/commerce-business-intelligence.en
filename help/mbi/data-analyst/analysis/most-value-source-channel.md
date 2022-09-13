---
title: Identifying Your Most Valuable Marketing Sources and Channels
zendesk_id: 360016732991
---

You researched your audience, you created your campaign, you invested in a few marketing channels. Now that some time has passed, how are those channels performing? What channel has brought in the most new users? What source has contributed the most to your total revenue?

With MBI, you can easily segment your revenue and users by referral source, whether it corresponds to [Google Analytics' UTM fields](https://support.google.com/analytics/answer/1191184?hl=en) or custom data fields. This segmentation will allow you to find your best performing channels and better invest your marketing budget.

In this article, we explore some reports that you can use to uncover your most valuable marketing channels:

* [New users by sources](../#newusersbysource)
* [Average lifetime revenue by user source](../#avglifetimerev)
* [Average order value by user source](../#avgorderval)
* [Revenue by user registration date and sources](../#revbyregdateandsource)
* [Repeat orders by user source](../#repeatordersbysource)

## Prerequisites {#prereqs}

To build the analyses in this article, you need access to marketing acquisition/referral source data. If you are not already tracking it, you will need to bring [order referral source data from Google ECommerce](../importing-data/integrations/google-ecommerce.md) into MBI before you can continue. In addition, adding user device information to your analyses enables you to see what technology your referrals are using.

## New users by source {#newusersbysource}

Assessing the performance of referral sources is key in determining your most valuable channels. This report shows you the number of newly registered users, by acquisition source, over time, thus allowing you to track the performance of referral sources in acquiring new registered users.

To create this report in the [Report Builder](../../tutorials/using-visual-report-builder.md), add the **New users** metric (or an equivalent metric that counts the number of new users over time) to the report. Then do the following:

1. Set the **Time Period** to the registration period you want to analyze.
1. Set the **Interval** to monthly.
1. Set **Group By** to acquisition (or referral) source and select the sources you want to include.
1. For this example, we used the **stacked columns** chart type.

Here is a visual walkthrough:

[ ![Creating a New users by source report.](../../assets/New_Users_by_source.gif){: style="max-width: 500px;"}][4]{: data-lightbox="image-1" data-title="Creating a New users by source report."}
*Click for a closer look!*

## Average lifetime revenue by user source {#avglifetimerev}

Finding the channels that bring in new users is important, but how valuable are those referrals overall? This report shows the average lifetime revenue of users from specific acquisition sources over time. In other words, this allows you to see whether users acquired from a particular source spend more with you over their lifetime than a group of users acquired from a different source.

To create this report in the Report Builder, add the **Average lifetime revenue** metric to the report. Then do the following:

1. Set the **Time Period** to the time period you want to analyze.
1. Set the **Interval** to monthly.
1. Set **Group By** to acquisition (or referral) source and select the sources you want to include.
1. For this example, we used the **line chart** type.

Here is a visual walkthrough:

[ ![Creating an Average lifetime revenue by user source.](../../assets/Lifetime_revenue_by_user_source.gif){: style="max-width: 500px;"}][5]{: data-lightbox="image-1" data-title="Creating an Average lifetime revenue by user source report."}
*Click for a closer look!*

This example only looks at lifetime revenue, but you could also replicate this analysis to look at the **Number of orders** or **Distinct buyers** by referral source.

## Average order value by user source {#avgorderval}

To get a better idea of how much money users from a specific acquisition source spend, you can build a report that looks at their Average order value. This will enable you to track whether users acquired from a particular source spend more per order than users from another source.

To create this report in the Report Builder, add the **Average order value** metric and then do the following:

1. Set the **Time Period** to the registration period you want to analyze.
1. Set the **Time Interval** to monthly.
1. Set **Group By** to acquisition (or referral) source and select the sources you want to include.
1. For this example, we used the **stacked columns** chart type.

Here is a visual walkthrough:

[ ![Creating an Average order value by user source report.](../../assets/Average_order_value_by_source.gif){: style="max-width: 500px;"}][6]{: data-lightbox="image-1" data-title="Creating an Average order value by user source report."}
*Click for a closer look!*

## Total revenue by user registration date and source {#revbyregdateandsource}

The lifetime revenue analysis we went over earlier lets you look at the average lifetime revenue of users acquired from different sources, but what about total lifetime revenue? This report will allow you to identify how much overall revenue users that registered during a specific time and from a specific source generate.

To create this report in the Report Builder, add the **Revenue by user registration date** metric. If you have not [created this metric](../../data-user/reports/ess-manage-data-metrics.md) already, you can do so by replicating the **Revenue** metric and **changing the time stamp to User's creation date**. After adding the metric, do the following:

1. Set the **Time Period** to the registration period you want to analyze.
1. Set the **Time Interval** to monthly.
1. Set **Group By** to acquisition (or referral) source and select the sources you want to include.
1. For this example, we used the **stacked columns** chart type.

Here is a visual walkthrough:

[ ![Creating a Total revenue by user registration date &amp; source report.](../../assets/Revenue_by_user_registration_date_and_source.gif){: style="max-width: 500px;"}][8]{: data-lightbox="image-1" data-title="Creating a Total revenue by user registration date &amp; source report."}
*Click for a closer look!*

## Repeat orders by user source {#repeatordersbysource}

The Average order value report shows you, on average, how much users acquired from a particular source spend when placing an order. This report, however, does not show you if those same users are repeat customers. But with the Repeat orders by users sources, you can see if users from a particular source make more or less repeat purchases.

To create this report in the [Report Builder](../../tutorials/using-visual-report-builder.md), add the **Number of orders** metric and then do the following:

1. Set the **Time Period** to the registration period you want to analyze.
1. Set the **Time Interval** to monthly.
1. Add a **filter** so that only users with repeat orders are included:

    *User's order number greater than 1

    *
1. Set **Group By** to acquisition (or referral) source and select the sources you want to include.
1. For this example, we used the **stacked columns** chart type.

Here is a visual walkthrough:

[ ![Creating a Repeat orders by user source report.](../../assets/Repeat_orders_by_user_source.gif){: style="max-width: 500px;"}][9]{: data-lightbox="image-1" data-title="Creating a Repeat orders by user source report."}
*Click for a closer look!*

## Wrapping Up {#wrapup}

In this article, we touched on just a few analyses you can use to analyze the value of your acquisition and marketing channels, but this is just the tip of the iceberg. If you created a powerful analysis we did not cover here, let us in on what you are doing in the comments.

## Related {#related}

* [Tracking order referral source via Google ECommerce](../importing-data/integrations/google-ecommerce.md)
* [Connecting your Google Adwords account](../importing-data/integrations/google-adwords.md)
* [Building Google ECommerce dimensions with orders and customer data](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
* [Best-practices for UTM tagging in Google Analytics](../../best-practices/utm-tagging-google.md)

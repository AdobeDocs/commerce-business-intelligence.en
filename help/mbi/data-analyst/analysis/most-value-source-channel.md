---
title: Identifying Your Most Valuable Marketing Sources and Channels
description: Learn about some reports that you can use to uncover your most valuable marketing channels.
exl-id: 8d25bc80-ea60-47db-b01b-04a23a24c14d
---
# Identify Successful Marketing Sources

You researched your audience, you created your campaign, you invested in a few marketing channels. Now that some time has passed, how are those channels performing? What channel has brought in the most new users? What source has contributed the most to your total revenue?

With [!DNL MBI], you can easily segment your revenue and users by referral source, whether it corresponds to [!DNL [Google Analytics' UTM fields]](https://support.google.com/analytics/answer/1191184?hl=en) or custom data fields. This segmentation allows you to find your best performing channels and better invest your marketing budget.

This article explores some reports that you can use to uncover your most valuable marketing channels:

* [New users by sources](#newusersbysource)
* [Average lifetime revenue by user source](#avglifetimerev)
* [Average order value by user source](#avgorderval)
* [Revenue by user registration date and sources](#revbyregdateandsource)
* [Repeat orders by user source](#repeatordersbysource)

## Prerequisites {#prereqs}

To build the analyses in this article, you need access to marketing acquisition/referral source data. If you are not already tracking it, you need to bring [order referral source data from [!DNL Google ECommerce]](../importing-data/integrations/google-ecommerce.md) into [!DNL MBI] before you can continue. In addition, adding user device information to your analyses enables you to see what technology your referrals are using.

## New users by source {#newusersbysource}

Assessing the performance of referral sources is key in determining your most valuable channels. This report shows you the number of newly registered users, by acquisition source, over time, thus allowing you to track the performance of referral sources in acquiring new registered users.

To create this report in the [Report Builder](../../tutorials/using-visual-report-builder.md), add the **New users** metric (or an equivalent metric that counts the number of new users over time) to the report. Then do the following:

1. Set the [!UICONTROL Time Period] to the registration period that you want to analyze.
1. Set the [!UICONTROL Interval] to monthly.
1. Set [!UICONTROL Group By] to acquisition (or referral) source and select the sources that you want to include.
1. This example uses the `stacked columns` [!UICONTROL chart type].

Here is a visual walkthrough:

![Creating a New users by source report.](../../assets/New_Users_by_source.gif)

## Average lifetime revenue by user source {#avglifetimerev}

Finding the channels that bring in new users is important, but how valuable are those referrals overall? This report shows the average lifetime revenue of users from specific acquisition sources over time. In other words, this allows you to see whether users acquired from a particular source spend more with you over their lifetime than a group of users acquired from a different source.

To create this report in the Report Builder, add the **Average lifetime revenue** metric to the report. Then do the following:

1. Set the [!UICONTROL Time Period] to the time period that you want to analyze.
1. Set the [!UICONTROL Interval] to monthly.
[!UICONTROL Group By] to acquisition (or referral) source and select the sources that you want to include.
1. This example uses the `line chart` type.

Here is a visual walkthrough:

![Creating an Average lifetime revenue by user source](../../assets/Lifetime_revenue_by_user_source.gif).

This example only looks at lifetime revenue, but you could also replicate this analysis to look at the [!UICONTROL Number of orders] or [!UICONTROL Distinct buyers] by referral source.

## Average order value by user source {#avgorderval}

To get a better idea of how much money users from a specific acquisition source spend, you can build a report that looks at their Average order value. This enables you to track whether users acquired from a particular source spend more per order than users from another source.

To create this report in the Report Builder, add the **Average order value** metric and then do the following:

1. Set the [!UICONTROL Time Period] to the registration period that you want to analyze.
1. Set the [!UICONTROL Time Interval] to monthly.
1. Set [!UICONTROL Group By] to acquisition (or referral) source and select the sources that you want to include.
1. This example uses the **stacked columns** chart type.

Here is a visual walkthrough:

![Creating an Average order value by user source report.](../../assets/Average_order_value_by_source.gif)

## Total revenue by user registration date and source {#revbyregdateandsource}

The lifetime revenue analysis that was covered earlier lets you look at the average lifetime revenue of users acquired from different sources, but what about total lifetime revenue? This report allows you to identify how much overall revenue users that registered during a specific time and from a specific source generate.

To create this report in the Report Builder, add the `Revenue by user registration date` metric. If you have not [created this metric](../../data-user/reports/ess-manage-data-metrics.md) already, you can do so by replicating the `Revenue` metric and changing the `time stamp` to User's `creation date`. After adding the metric, do the following:

1. Set the [!UICONTROL Time Period] to the registration period that you want to analyze.
1. Set the [!UICONTROL Time Interval] to monthly.
1. Set [!UICONTROL Group By] to acquisition (or referral) source and select the sources that you want to include.
1. This example uses the `stacked columns` chart type.

Here is a visual walkthrough:

![Creating a Total revenue by user registration date &amp; source report.](../../assets/Revenue_by_user_registration_date_and_source.gif)

## Repeat orders by user source {#repeatordersbysource}

The Average order value report shows you, on average, how many users acquired from a particular source spend when placing an order. This report, however, does not show you if those same users are repeat customers. But with the Repeat orders by users sources, you can see if users from a particular source make more or less repeat purchases.

To create this report in the [Report Builder](../../tutorials/using-visual-report-builder.md), add the **Number of orders** metric and then do the following:

1. Set the [!UICONTROL Time Period] to the registration period that you want to analyze.
1. Set the [!UICONTROL Time Interval] to monthly.
1. Add a [!UICONTROL filter] so that only users with repeat orders are included:

    User's order number greater than 1

1. Set [!UICONTROL Group By] to acquisition (or referral) source and select the sources that you want to include.
1. This example uses the `stacked columns` chart type.

Here is a visual walkthrough:

![Creating a Repeat orders by user source report.](../../assets/Repeat_orders_by_user_source.gif)


## Wrapping Up {#wrapup}

This article touched on just a few analyses you can use to analyze the value of your acquisition and marketing channels, but this is just the tip of the iceberg. 

## Related {#related}

* [Tracking order referral source via [!DNL Google ECommerce]](../importing-data/integrations/google-ecommerce.md)
* [Connecting your [!DNL Google Adwords] account](../importing-data/integrations/google-adwords.md)
* [Building [!DNL Google ECommerce] dimensions with orders and customer data](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
* [Best practices for UTM tagging in [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)

---
title: Included Dashboards
description: Learn how to check on the health of essential metrics such as user lifetime revenue, number of repeat purchases, and more, thus creating a solid foundation for future exploration.
exl-id: f50fc417-e5d4-401c-9baa-cda1468196a2
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
TQID: https://experienceleague.adobe.com/P-wLLeYV4VVlaeMEa-X5WkXcS09d5fKQZGQwGO-OnK0
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
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: beb7a3c1-66ab-4786-b879-7621375b3c40
    internal-label: Email marketing
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
---
# Included dashboards

[!DNL Adobe] offers `eCommerce` and `SaaS` Starter Packages. These packages, created by Adobe analysts, contain a customized set of dashboards and reports for your dataset. The analyses contained in these packages let you check on the health of essential metrics such as user lifetime revenue, number of repeat purchases, and more, thus creating a solid foundation for future exploration.

>[!NOTE]
>
>The availability of some dashboards depends upon your dataset.

If you have questions or you are interested in adding a package to your account, submit a [support ticket](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) for help.

## Executive overview

The `executive overview` dashboard is built from charts that exist on other dashboards. This dashboard is a high-level overview of your data and contains charts that would be reviewed daily, while other dashboards contained more detailed information. Initially, it is set as the default dashboard in each account.

A general set of charts is included for you. Adobe recommends that you tailor this dashboard to your needs by adding other charts you use most frequently.

## Cohort analysis

The `cohort analysis` dashboard includes a set of charts that show the average user lifetime revenue growth and incremental revenue growth grouped by registration cohorts. This reveals whether customer lifetime value (LTV), the value of a customer to a business, increases over time, and also identifies trends around LTV growth. By default, *all registered users (buyers and non-buyers) are accounted for* in the average LTV calculation - see the [cohort analysis topic](../../data-analyst/dev-reports/cohort-rpt-bldr.md).

This dashboard may also include cohort charts that analyze the lifetime revenue of users from a specific acquisition source, channel, or demographic (for example, New York or California). This is to demonstrate how you can analyze LTV for specific segments of your user base and seeing whether one group or another yields higher LTV over time.

For more information on cohorts, see [Performing Cohort Analysis](../../data-analyst/dev-reports/cohort-rpt-bldr.md).

If you are currently not tracking user acquisition source, see the [Track User Acquisition Source Data Overview](../../data-analyst/analysis/google-track-user-acq.md).

## Email summary

The `Email Summary` dashboard includes a sample set of charts that can be used in an automated daily email summary. Refer to [creating automated email summaries](../../data-user/export-data/email-summaries.md) for more information on configuring email summaries.  

## Retention health

The `Retention health` dashboard reveals your user base's repeat purchase behavior.

The `Time between orders` chart shows the average and/or median elapsed time between a user' first and second order, second and third order, and so on. You might consider using this data to configure your email marketing campaigns.

The `Users by lifetime number of orders` chart lists the total number of users for each lifetime number of orders to provide a general overview of repeat purchase behavior.  

The `Repeat order probability` chart shows the likelihood of a user with a certain order number to make a repeat purchase. To see the probability of customers that made `x` orders to make `(x+1)` orders, simply divide the number of people who've made at least `(x+1)` purchases by the number of people who have made at least `x` purchases.

### Example

Number of customers who made one purchase in their lifetime: `90`

Number of customers who made two purchases in their lifetime: `30`

Number of customers who made three purchases in their lifetime: `10`

In this example, the repeat order probability of customers who have made one purchase in their lifetime to make a second purchase is: `(30 + 10) / (30+10+90) = 30.77%`.

## Customer LTV growth

The `Customer LTV growth` dashboard includes a set of charts that finds the average revenue per user. The charts are segmented based on the average revenue being generated within either the first 30, 60, 90, or 365 days after registration.  

The bottom row of charts shows that these averages segmented by acquisition sources or demographics to reveal which groups of users generate the most revenue over time.

## Product performance

The `Product Performance` dashboard includes charts that reveal general product performance by displaying the number of items sold and revenue by item, and identifying top performing products.

## Recent activity

The `Recent Activity` dashboard shows performance data for the past 30 days.

## Transactional health

The `Transaction Health` dashboard includes overview charts of revenue, orders, and average order value. These charts may be segmented by marketing channels, demographics, or by special coupon codes.

## Users to target

The `Users to target` dashboard includes table-style charts that list users with specific purchasing behaviors in common. A few examples include:

* List of one-time buyers that purchase `X` months ago (who you may want to reactivate)

* List of top spenders (who you may want to keep happy)

* List of top spenders that were active in the past `X` days (who you may want to reward)

You can use your data export tools to create email lists of users with similar purchasing behavior for target marketing.

## User activity

The `User activity` dashboard includes charts that segment users by various data, including acquisition source, demographics, and average first time to order. It also includes user cohort analysis, including the overall average lifetime revenue by users' registration month.

The `% of cohort members who have purchased` chart is valuable, because it shows the conversion ratio (from 0 through 1) of users based on when they register (each line represents a cohort of users). It also shows when they make their first purchase (for example, in month 1, 2, 3... after registration). This may show you that 10% of users activated in month 1, while this number grows in month 2, 3, 4... and may plateau later on.

Typically, the lines in this chart become horizontal after some period in time. This indicates that few additional cohort members are converting organically after that point - most users who are going to make a purchase have already done so. At this point, these members are highly unlikely to convert to purchasers without intervention. Reaching out to them with custom promotions or targeted emails is a low-risk way to jump-start conversion of this population.

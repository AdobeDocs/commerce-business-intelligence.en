---
title: Average time to first purchase report
description: Learn how to use the Average time to first purchase report.
exl-id: c18734ce-0ae0-4e84-b9d0-eb2c21a5c3a5
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
TQID: https://experienceleague.adobe.com/LWbb4E4IMPQd-hUpsylSGt4lgrrvYI1VUhmovjvcfu4
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
---
# Average time to first purchase report 

Many Adobe customers have a metric and chart named `Average time to first purchase`, which shows the average time between a group of users' registration date and first purchase date. The data almost invariably slopes downward as time moves closer to the present.

![average time to first order](../../assets/average-time-to-first-order.png)

This is because these newer customers have not yet had the opportunity to generate any purchases that were made more than one month from their join date. Since users who have never made a purchase are not included at all (until they do make a purchase), this biases the average downward for newer groups of customers.

There are a few other potential ways to look at this metric that introduce less bias. Explore one example.

## Example: Perform a `cohort` analysis of first orders

You may have a chart on your `Users` dashboard named `Time to first order cohort`. This report uses the `Distinct buyers` metric, groups users by `cohort` weeks or months of registration, and shows the ratio (between `0` and `1`) of users that made a first purchase in the following weeks or months after registration.

The chart may show that for users that registered in December 2014, `0.56` (or `56%`) made a first order by month 2 (for example, January 2015).

This cohort analysis is a good indicator of user activation rate over time. If this chart starts to flatten or plateau, and you are still not near 100% conversion to buyers, it may be time to activate the remaining users via email campaigns.

---
title: Optimizing Your Database for Analysis
description: Learn how to optimize your database for analysis.
exl-id: e73e1a1e-c933-476d-97bc-bd8f52bb2fa1
role: Admin, Developer, User
feature: Business Performance, Data Integration, Data Import/Export, Data Warehouse Manager
TQID: https://experienceleague.adobe.com/5UkWGr-YOIfCy-BSomo2HWexXd-oM9ONvXpJkzyTPT0
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
  - id: b5f00040-57a0-4a6d-a39e-383b1936c2c9
    internal-label: Compliance
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
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
    internal-label: Insights
---
# Optimize your database

The primary benefit of using an operational database for [!DNL Adobe Commerce Intelligence] is that nothing needs to be built or modified in order to collect data. Valuable information is already there - you just need to unlock it.

This topic contains some recommendations to help you optimize your database for analysis and draw actionable insights from raw data.

## Do Not Delete Data

>[!TIP]
>
>The local and international laws that affect your business (and your own terms of service) may affect what types of data you can retain and how long you can retain it for. Compliance with these laws should be your first priority.

When an order is cancelled, a user deactivates their account, or a product is discontinued, it is tempting to delete the associated information in the database. Tables grow and eliminating clutter seems like a prudent idea. However, deleting rows means that this information is lost forever or that you need to dig through old backups to find it.

Instead, you can add a status column to the table which indicates when the row is no longer active or relevant. It is also recommended to add a column that stores the date the change was made, or create a log for historical changes. If tables grow large enough that performance begins to suffer, consider archiving the old data to a table used for analytics.

## Rarely Overwrite Data

Overwriting data should be done sparingly and with caution.

Using login dates as an example, many companies store the last login date rather than a table of historical logins. While you may only need the last login date for functional purposes, that overwritten data is a huge loss from an analytics perspective. Not keeping a complete log of these actions eliminates the ability to see how many users stayed away for long periods of time and then reactivated. It also makes it impossible to build things like user engagement cohort analyses based on logins.

Generally, if you are updating a record due to some kind of user action, do not overwrite information about a previous or separate user action.

## Include `Updated_at` Columns for Data Updated Over Time

If a table's rows will have changing values over time, for example, **order\_status** changes from`processing` to `complete`, include an **updated\_at** column to record when the latest change occurs. Ensure that an **updated\_at** value is available when first inserting the new data row, when the **updated\_at** date corresponds to the **created\_at** date.

In addition to optimizing for analysis, **updated\_at** columns also allow you to use [Incremental Replication methods](../data-analyst/data-warehouse-mgr/cfg-replication-methods.md), which can help shorten the length of your update cycles. 

## Store User Acquisition Source

One of the most common mistakes is the [user acquisition source](../data-analyst/analysis/google-track-user-acq.md) (UAS) not being stored in the operational database. In most situations when this is an issue, UAS is only being tracked through [!DNL Google Analytics] or some other web analytics tool. While these tools can be valuable, there are some drawbacks to storing UAS in them exclusively; such as, you cannot extract user-level data from these tools. When it is possible, it is usually a difficult process. It should be easy to get this information and marry it with data from other sources, such as the behavioral and transactional information also stored in your database.

Storing UAS in your own database is often the largest improvement that an online business can make to its analytical capabilities. This allows for the analysis of sales, user engagement, payback periods, customer lifetime value, churn, and other critical metrics by UAS. [This data is crucial when deciding where to invest marketing resources](../data-analyst/analysis/most-value-source-channel.md).

Too many companies focus solely on finding channels that provide new users at the lowest cost. If you are not tracking the quality of users acquired from each channel, you run the risk of attracting users who do not generate business value.

## Data Table Setup

### Set a Primary Key

A [primary key](https://en.wikipedia.org/wiki/Unique_key) is an unchanging column (or set of columns) that produces unique values within a table. Primary keys are incredibly important, as they ensure that your tables are properly replicated in [!DNL Commerce Intelligence].

When building primary keys, use an integer data type for the column that auto-increases. Adobe recommends you avoid using multiple column primary keys where possible.

If your table is an SQL view, add a column that can act as a primary key. [!DNL Commerce Intelligence] is able to automatically identify this column as a primary key.

### Assign a Data Type to Your Data Column

If a data column does not have an assigned [data type](https://en.wikipedia.org/wiki/Data_type), [!DNL Commerce Intelligence] guesses which data type to use. If the system guesses incorrectly, you may not be able to perform the relevant analyses until the Adobe support team adjusts the column to the proper data type. For example, if a date column is guessed as a numeric data type, you can trend over time using that date dimension.

### Add Prefixes to Your Data Tables if You Have Multiple Databases

If you have more than one database connected to [!DNL Commerce Intelligence], Adobe recommends you add prefixes to your tables to avoid confusion. Prefixes help you remember where metrics or data dimensions are sourced from.

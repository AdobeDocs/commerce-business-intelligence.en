---
title: Optimizing Your Database for Analysis
description: Learn how to optimize your database for analysis. 
---
# Optimize your database

The primary benefit of using an operational database for business intelligence is that nothing needs to be built or modified in order to collect data. Valuable information is already there; all you need to do is unlock it.

This topic contains some recommendations to help you optimize your database for analysis and draw actionable insights from raw data.

## Do Not Delete Data

>[!TIP]
>
>The local and international laws that affect your business (and your own terms of service) may affect what types of data you can retain and how long you can retain it for. Compliance with these laws should be your first priority.

When an order is cancelled, a user deactivates their account, or a product is discontinued, it is tempting to delete the associated information in the database. Tables grow and eliminating clutter seems like a prudent idea. However, deleting rows means that this information is lost forever or that you will need to dig through old backups to find it.

Instead, you can add a status column to the table which will indicate when the row is no longer active or relevant. It is also recommended to add a column that stores the date the change was made, or create a log for historical changes. If tables grow large enough that performance begins to suffer, consider archiving the old data to a table used for analytics.

## Rarely Overwrite Data

Overwriting data should be done sparingly and with caution.

Using login dates as an example, many companies will store the last login date rather than a table of historical logins. While you may only need the last login date for functional purposes, that overwritten data is a huge loss from an analytics perspective. Not keeping a complete log of these actions eliminates the ability to see how many users stayed away for long periods of time and then reactivated. It also makes it impossible to build things like user engagement cohort analyses based on logins.

As a general rule, if you are updating a record due to some kind of user action, do not overwrite information about a previous or separate user action.

## Include Updated_at Columns for Data Updated Over Time

If a table's rows will have changing values over time, for example, **order\_status** changes from`processing` to `complete`, include an **updated\_at** column to record when the latest change occurs. Ensure that an **updated\_at** value is available when first inserting the new data row, at which time the **updated\_at** date corresponds to the **created\_at** date.

In addition to optimizing for analysis, **updated\_at** columns also allow you to use [Incremental Replication methods](../data-analyst/data-warehouse-mgr/cfg-replication-methods.md), which can help shorten the length of your update cycles. 

## Store User Acquisition Source

One of the most common mistakes is the [user acquisition source](../data-analyst/analysis/google-track-user-acq.md) (UAS) not being stored in the operational database. In the majority of situations where this is an issue, UAS is only being tracked through [!DNL Google Analytics] or some other web analytics tool. While these tools can be extremely valuable, there are some drawbacks to storing UAS in them exclusively; such as, you cannot extract user-level data from these tools. When it is possible, it is usually a difficult process. It should be easy to get this information and marry it with data from other sources, such as the behavioral and transactional information also stored in your database.

Storing UAS in your own database is often the largest improvement an online business can make to its analytical capabilities. This allows for the analysis of sales, user engagement, payback periods, customer lifetime value, churn, and other critical metrics by UAS. [This data is crucial when deciding where to invest marketing resources](../data-analyst/analysis/most-value-source-channel.md).

Too many companies focus solely on finding channels that provide new users at the lowest cost, but if you are not tracking the quality of users acquired from each channel, you run the risk of attracting users who do not generate business value.

## Data Table Setup

### Set a Primary Key

A [primary key](http://en.wikipedia.org/wiki/Unique_key) is an unchanging column (or set of columns) that produces unique values within a table. Primary keys are incredibly important, as they ensure that your tables are properly replicated in MBI.

When building primary keys, use an integer data type for the column that auto-increases. We also recommend you avoid using multiple column primary keys where possible.

If your table is an SQL view, add a column that can act as a primary key. [!DNL MBI] will be able to automatically identify this column as a primary key.

### Assign a Data Type to Your Data Column

If a data column does not have an assigned [data type](http://en.wikipedia.org/wiki/Data_type), [!DNL MBI] will guess what data type to use. If the system guesses incorrectly, you may not be able to perform the relevant analyses until our support team adjusts the column to the proper data type. For example, if a date column is guessed as a numeric data type, you are be able to trend over time using that date dimension.

### Add Prefixes to Your Data Tables if You Have Multiple Databases

If you have more than one database connected to [!DNL MBI], we recommend you add prefixes to your tables to avoid confusion. Prefixes will help you remember where metrics or data dimensions are sourced from.

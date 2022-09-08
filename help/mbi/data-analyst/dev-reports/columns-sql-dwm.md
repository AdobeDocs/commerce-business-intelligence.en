---
title: Differences in Columns Between SQL and Data Warehouse Manager
zendesk_id: 360016506212
---

There are two key differences between columns created in the [SQL Report Builder](../data-analyst/dev-reports/sql-rpt-bldr.md) and those created using the [Data Warehouse Manager](../data-analyst/data-warehouse-mgr/creating-calculated-columns.md): one is the dependency on update cycles, the other is how columns are saved in your account.

## Columns in the SQL Report Builder

Columns are not dependent on update cycles, so you no longer have to wait for one to complete before you can iterate on your column. If you make a mistake, it only takes a few keystrokes to correct it - no more waiting for two updates to wrap up before you can get back to work.

It’s important to note that the columns you create using the SQL editor are not saved to your Data Warehouse. You’ll always have access to the query containing the column, but if you want to use the column in more than one report, you’ll have to recreate it in the query for each report. **This means that columns created using the SQL editor cannot be used in the traditional Report Builder.**

## Columns in the Data Warehouse Manager

Columns are dependent on update cycles, so a full cycle must complete before they can be edited. These columns are saved to the Data Warehouse Manager and can be used in the traditional Report Builder or SQL Report Builder.

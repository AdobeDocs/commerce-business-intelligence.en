---
title: Formatting and Importing Financial Data
zendesk_id: 360016505472
---

This topic discusses the best way to import financial data for analysis in Magento BI.

A two-dimensional crosstab data table is often the format used for financial data. With values categorized by labels in both columns and rows, this type of layout might be easy to view with human eyes and spreadsheet tools, but it isn’t very friendly to databases.

![]({% link images/crosstab.png %})

To import and analyze this data in Magento BI, the table must be flattened into a one-dimensional list. When flattened, each data value is categorized by multiple labels that are all in a single row, where each row is unique or would have a unique identifier, for example a primary key column)

![]({% link images/flattened.png %})

## Formatting Excel files for Import

To flatten a two-dimensional table using an Excel pivot table:

1. Open the file with the two-dimensional data table.
1. Open the PivotTable Wizard. In Windows, the shortcut is `Alt-D`, in Mac OSX, enter `Command-Option-P`.
1. Select **Multiple consolidated ranges** and click **Next**.
1. Select **I will create the page fields** and click **Next**.
1. Select the entire data set in the two-dimensional table, including the labels. Ensure that zero is selected for the number of desired page fields and click **Next**.
1. Create the pivot table in a new sheet and click **Finish**.
1. Deselect the column and row fields from the field list.
1. Double-click the resulting numerical value to show the flattened source data in a new sheet.
    ![]({% link images/pivot-table-double-click.png %})
1. Save as a **CSV** file.

That\'s it! The data table has been converted to a list format, preserving all of its original information, and can now be [imported to Magento BI]({% link data-analyst/importing-data/connecting-data/using-file-uploader.md %}) for analysis.

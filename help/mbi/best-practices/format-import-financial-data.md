---
title: Formatting and Importing Financial Data
description: Learn how to format and import financial data.
exl-id: cdbed262-7cf1-4fd6-ad5a-c44d26dffba7
role: Admin, Developer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
TQID: https://experienceleague.adobe.com/O1WKa98rRVw1dcgNQPsORit2gmZNn1Wi7H-Q4J7KcA0
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
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
---
# Format and Import Financial Data

This topic discusses the best way to import financial data for analysis in [!DNL Adobe Commerce Intelligence].

A two-dimensional, cross-tab data table is often the format used for financial data. With values categorized by labels in both columns and rows, this type of layout might be easy to view with human eyes and spreadsheet tools, but it is not friendly to databases.

![Crosstab format showing data in pivot table layout](../../mbi/assets/crosstab.png)

To import and analyze this data in [!DNL Commerce Intelligence], the table must be flattened into a one-dimensional list. When flattened, each data value is categorized by multiple labels that are all in a single row, where each row is unique or would have a unique identifier, for example a primary key column.

![Flattened format showing data in columnar layout](../../mbi/assets/flattened.png)

## Formatting Excel files for Import

To flatten a two-dimensional table using an [!DNL Excel] pivot table:

1. Open the file with the two-dimensional data table.
1. Open the PivotTable Wizard. In [!DNL Windows], the shortcut is `Alt-D`. In [!DNL Mac OS], enter `Command-Option-P`.
1. Select **[!UICONTROL Multiple consolidated ranges]** and click **[!UICONTROL Next]**.
1. Select **[!UICONTROL I will create the page fields]** and click **[!UICONTROL Next]**.
1. Select the entire data set in the two-dimensional table, including the labels. Ensure that `0` is selected for the number of desired page fields and click **[!UICONTROL Next]**.
1. Create the pivot table in a new sheet and click **[!UICONTROL Finish]**.
1. Deselect the column and row fields from the field list.
1. Double-click the resulting numerical value to show the flattened source data in a new sheet.
    ![Excel pivot table field list showing double-click to expand](../../mbi/assets/pivot-table-double-click.png)
1. Save as a `CSV` file.

## Wrapping Up

The data table has been converted to a list format, preserving all of its original information, and can now be [imported to [!DNL Commerce Intelligence]](../data-analyst/importing-data/connecting-data/using-file-uploader.md) for analysis.

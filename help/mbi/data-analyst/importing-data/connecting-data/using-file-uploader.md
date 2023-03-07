---
title: Use File Uploader
description: Learn how to put all of your data into a single Data Warehouse.
exl-id: 28db0e78-0222-431d-bbb9-6ef133686603
---
# Use File Uploader

>[!NOTE]
>
>Requires [Admin permissions](../../../administrator/user-management/user-management.md).

[!DNL MBI] is powerful not only because of its visualization features, but because it gives you the ability to put all of your data into a single Data Warehouse. Even data that lives outside your databases and integrations can be brought into [!DNL MBI] by using the File Upload tool in the Data Warehouse Manager.

Let us use ad campaigns as an example. If you are running both online and offline campaigns, you cannot get the whole picture if you are only analyzing data from an online integration. Uploading a spreadsheet with the offline campaign data allows you to analyze both sets of data and get a more robust understanding of your campaign performance.

## Restrictions and requirements {#require}

1. **The only supported format for file uploads is `CSV` or `comma separated values`**. If you are working in Excel, you can use the Save As function to save the file in `.csv` format.
1. **`CSV` files must use `UTF-8 encoding`**. Most the time, this is not an issue. If you encounter this error while uploading a file, [consult this Support article](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/resolving-utf-8-errors-for-csv-file-uploads.html?lang=en).
1. **Files cannot be larger than 100MB**. If the file is larger than this, separate the table into chunks and save them as individual files. You can append the data after the initial file is loaded.
1. **All tables must have a `primary key`**. There needs to be at least one column in your table that can be used as a `primary key`, or a unique identifier for each row in the table. Any column designated as a `primary key` can *never* be null. A `primary key` can be as simple as adding a column that gives a number to each row, or can be two columns concatenated to make a column of unique values (for example, `campaign name` and `date`).

     If a column (or columns) is designated as unique but there are duplicates, the duplicate rows are not imported.

## Formatting data for upload {#formatting}

Before you can upload your data into [!DNL MBI], check that it is formatted according to the guidelines in this section.

### Header row {#header}

To ensure that columns are labeled and imported properly, make sure that the first row of your spreadsheet is a header that describes the data in each column.

Column names must be unique and contain only letters, numbers, spaces, and these symbols: `$ % # /`. If a column name contains a comma, it is split into two columns when the file uploads. Also, Adobe recommends that there be fewer than 85 columns in the file to optimize update speed.

### Data with commas {#commas}

Because files have to be in `CSV` format, the use of commas can cause problems with uploading data. `CSV` files use commas to indicate new values, therefore a column with a name like `Campaigns`, `August` is read as two columns (`Campaigns` and `August`) instead of one, shifting all of your data over one row. Adobe recommends avoiding commas wherever possible. You can use `Data Preview` to see if your data is displaying correctly once an update completes.

### Dates

Any dataset that includes dates must use the [standard date format](https://dev.mysql.com/doc/refman/5.7/en/datetime.html) `YYYY-MM-DD HH:MM:SS` or `MM/DD/YYYY`.

### Special Characters

Some special characters are not accepted. For example, the pipe symbol `& # 1 2 4` is interpreted as creating a column and causes errors when uploading a file.

### Decimal Numbers

Currency values should have the datatype `Decimal Number` selected, and these columns automatically round to two decimal places in your Data Warehouse. If you do not want to round your decimal numbers or have a degree of precision greater than this, you should select the `Non-Currency Decimal Number` datatype.

### Percentages

Percentages must be entered as decimals. For example:

| **Right:** | **Wrong:** |
|-----|-----|
| `.05` | `5%` |
| `.23` | `23` |

{style="table-layout:auto"}

### Values with leading and/or trailing zeroes {#zeroes}

Some values in your file - like ZIP codes and IDs - may begin or end with zeroes. To ensure that the zeroes are properly retained and uploaded, you can change the formatting type (for example, [from number to text](https://support.microsoft.com/en-us/office/format-numbers-as-text-583160db-936b-4e52-bdff-6f1863518ba4?ui=en-us&rs=en-us&ad=us)) or enforce number formatting.

Let us use `US ZIP codes` as an example of how to change number formatting. In [!DNL Excel], highlight the column containing `ZIP codes` and [change the number format](https://support.microsoft.com/en-us/office/display-numbers-as-postal-codes-61b55c9f-6fe3-4e54-96ca-9e85c38a5a1d?ui=en-us&rs=en-us&ad=us) to `ZIP code`. You can also select a custom number format, and in the `Type` window, enter `00000`. Keep in mind this method could present problems if some codes are formatted as `00000` and others are `00000-0000`.

The `Type` can be [formatted differently to accommodate other data types](https://support.microsoft.com/en-us/office/keeping-leading-zeros-and-large-numbers-1bf7b935-36e1-4985-842f-5dfa51f85fe7?correlationid=e1d4c2d3-cd5d-4a14-999d-437800274a90&ui=en-us&rs=en-us&ad=us), such as IDs. If an `ID` is nine digits long, for example, the `Type` could be `000000000` or `000-000-000`. This would change `123456` to `000-123-456`.

For [!DNL Google Docs] and [!DNL Apple Numbers] resources, refer to the [Related](#related) list at the bottom of this page.

## Uploading data {#uploading}

Now that your spreadsheet is correctly formatted and [!DNL MBI]-friendly, Let us add it to your Data Warehouse.

1. To get started, go to **[!UICONTROL Data** > **File Uploads]**.

1. Click the **[!UICONTROL Upload to New Table]** tab.

1. Click **[!UICONTROL Choose File]** and select the file. Click **[!UICONTROL Open]** to start the upload.

   After the upload completes, a list of the columns [!DNL MBI] found in your file displays.

1. Check that the column names and data types are correct. Specifically, check that any date columns are being read as dates and not numbers.

   >[!NOTE]
   >
   >The `datatype` is important, so do not skip this step!

1. Select the column (or columns) that make up the `primary key` for the table by using the checkboxes under the key icon.

1. Name the table.

1. Click **[!UICONTROL Save Table]**.

  A *Success!* message appears at the top of the screen after your table is saved.

If you need a visual, look at the whole process:

![](../../../assets/fileupload.gif)

Uploaded tables display under the **File Uploads** section of the table list (in both the All Tables and Synced Tables options) in the Data Warehouse Manager:

![](../../../assets/upload-tables.png)

## Updating or appending data to an existing table {#appending}

Got some new data to add to a file you have already uploaded? No problem - you can easily update and append data in [!DNL MBI].

1. To get started, go to **[!UICONTROL Manage Data** > **File Uploads]**.

1. Click the **[!UICONTROL Edit/Upload `.csv` to Existing Tables]** tab.

1. In the dropdown, click the name of the table you want to update or append.

1. Use the dropdown to select the option for handling duplicate rows:

    | | |
    |---|---|
    |`Overwrite old row with new row`|This overwrites existing data with new data if a row has the same primary key in both the existing table and the new file. This is the method to use for columns with values that change over time - for example, a Status column. Existing data is overwritten and updated with the new data. Rows with primary keys not in the existing table are added as new rows.|
    |`Retain old row; discard new row`|This causes new data to be ignored if a row has the same primary key in both the existing table and the new file.|
    |`Purge all existing rows first and ignore duplicate keys within the file`|This deletes any existing data and replaces it with the new data from the file. Only use this option if you do not need any of the data in the existing table.|

1. Click **[!UICONTROL Choose File]** and select the file.

1. Click **[!UICONTROL Open]** to start the upload.

    After the upload completes, [!DNL MBI] will validate the data structure in the file. A *Success!* message appears at the top of the screen after your table is saved.

## Data availability {#availability}

Just like calculated columns, data from file uploads is available after the next update cycle completes. If an update was in progress during the file upload, the data will not be available until after the next update. Once an update cycle is completed, you can navigate to the `Data Preview` tab in your Data Warehouse to ensure that the file uploaded correctly and data is displaying as expected.

## Wrapping up {#wrapup}

This article covered only the basics for using importing data, but you may want to do something more advanced. Check out the Related articles for guidance on formatting and importing financial, eCommerce, ad spend, and other types of data.

Also, file upload is not the only way to get your data into [!DNL MBI]. The [Data Import API](https://developer.adobe.com/commerce/services/reporting/import-api/) functions allow you to push arbitrary data into your [!DNL MBI] Data Warehouse.

## Related {#related}

* [Formatting and importing financial data](../../../best-practices/format-import-financial-data.md)
* [Importing offline / other ad spend data](../connecting-data/import-offline-ad-data.md)
* [Expected[!DNL Google ECommerce] data](../integrations/google-ecommerce-data.md)

## Third-Party Resources

* [Numbers Data Formatting Guide](http://www.dummies.com/how-to/content/how-to-choose-a-number-format-in-your-numbers-spre.html)
* [[!DNL Google Docs] Data Formatting Guide](https://support.google.com/docs/answer/56470?hl=en)

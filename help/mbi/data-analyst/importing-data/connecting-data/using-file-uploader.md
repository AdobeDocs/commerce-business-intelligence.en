---
title: Use File Uploader
description: Learn how to put all of your data into a single data warehouse.
---
# Use File Uploader

>[!NOTE]
>
>[Requires Admin permissions.](../../../administrator/user-management/user-management.md)

MBI is powerful not only because of its visualization features, but because it gives you the ability to put all of your data into a single data warehouse. Even data that lives outside your databases and integrations can be brought into MBI by using the File Upload tool in the Data Warehouse Manager.

Let us use ad campaigns as an example. If you are running both online and offline campaigns, you cannot get the whole picture if you are only analyzing data from an online integration. Uploading a spreadsheet with the offline campaign data allows you to analyze both sets of data and get a more robust understanding of your campaign performance.

## Restrictions and requirements {#require}

1. **The only supported format for file uploads is CSV, or comma separated values**. If you are working in Excel, you can use the Save As function to save the file in CSV format.
1. **CSV files must use UTF-8 encoding**. The majority of the time, this will not be an issue. If you encounter this error while uploading a file, [consult this Support article](https://support.magento.com/hc/en-us/articles/360016730591).
1. **Files cannot be larger than 100MB**. If the file is larger than this, separate the table into chunks and save them as individual files. You can use append the data after the initial file is loaded.
1. **All tables must have a primary key**. There needs to be at least one column in your table that can be used as a primary key, or a unique identifier for each row in the table. Any column designated as a primary key can *never* be null. A primary key can be as simple as adding a column that gives a number to each row, or can be two columns concatenated to make a column of unique values (e.g., campaign name + date).

     If a column (or columns) are designated as unique but there are duplicates, the duplicate rows will not be imported.

## Formatting data for upload {#formatting}

Before you can upload your data into MBI, check that it is formatted according to the guidelines in this section.

### Header row {#header}

To ensure that columns are labeled and imported properly, make sure the first row of your spreadsheet is a header that describes the data in each column.

Column names must be unique and contain only letters, numbers, spaces and these symbols: `$ % # /`. If a column name contains a comma, it will be split into two columns when the file uploads. Additionally, we recommend that there be less than 85 columns in the file to optimize update speed.

### Data with commas {#commas}

Because files have to be in CSV format, the use of commas can cause problems with uploading data. CSV files use commas to indicate new values, therefore a column with a name like Campaigns, August will be read as two columns (Campaigns and August) instead of one, shifting all of your data over one row. We recommend avoiding commas wherever possible. You can use Data Preview to see if your data is displaying correctly once an update completes.

### Dates

Any dataset that includes dates must use the [standard date format](https://dev.mysql.com/doc/refman/5.7/en/datetime.html) (YYYY-MM-DD HH:MM:SS) or MM/DD/YYYY.

### Special Characters

Some special characters are not accepted. For example, the pipe symbol "&#124;" is interpreted as creating a new column and will cause errors when uploading a file.

### Decimal Numbers

Currency values should have the datatype **Decimal Number** selected, and these columns will automatically round to two decimal places in your data warehouse. If you do not want to round your decimal numbers or have a degree of precision greater than this, you should select the **Non-Currency Decimal Number** datatype.

### Percentages

Percentages must be entered as decimals. For example:

| **Right:** | **Wrong:** |
|-----|-----|
| .05 | 5% |
| .23 | 23 |

{style="table-layout:auto"}

### Values with leading and/or trailing zeroes {#zeroes}

Some values in your file - like ZIP codes and IDs - may begin or end with zeroes. To ensure the zeroes are properly retained and uploaded, you can change the formatting type (i.e., [from number to text](https://support.office.com/en-US/article/format-numbers-as-text-583160db-936b-4e52-bdff-6f1863518ba4)) or enforce number formatting.

Let us use **US ZIP codes** as an example of how to change number formatting. In Excel, highlight the column containing ZIP codes and [change the number format](https://support.office.com/en-za/article/Display-numbers-as-postal-codes-61b55c9f-6fe3-4e54-96ca-9e85c38a5a1d) to "ZIP code". You can also select a custom number format, and in the Type window, enter "00000". Keep in mind this method could present problems if some codes are formatted as 00000 and others are 00000-0000.

The Type can be [formatted differently to accommodate other data types](https://support.office.com/en-us/article/Keep-leading-zeros-in-number-codes-1bf7b935-36e1-4985-842f-5dfa51f85fe7?CorrelationId=e1d4c2d3-cd5d-4a14-999d-437800274a90&ui=en-US&rs=en-US&ad=US), such as IDs. If an ID is nine digits long, for example, the Type could be "000000000" or "000-000-000". This would change "123456" to "000-123-456".

For Google Docs and Apple Numbers resources, refer to the [Related](#related) list at the bottom of this page.

## Uploading data {#uploading}

Now that your spreadsheet is correctly formatted and MBI-friendly, Let us add it to your data warehouse.

1. To get started, go to **Data > File Uploads**.

1. Click the **Upload to New Table** tab.

1. Click the **Choose File** button and select the file. Click **Open** to start the upload.

   After the upload completes, you will see a list of the columns MBI found in your file.

1. Check that the column names and data types are correct. Specifically, check that any date columns are being read as dates and not numbers.

   **The datatype is extremely important, so do not skip this step!**

1. Select the column (or columns) that will make up the primary key for the table by using the checkboxes under the key icon.

1. Name the table.

1. Click **Save Table**.

  A *Success!* message appears at the top of the screen after your table is saved.

If you need a visual, Here is a look at the whole process:

![](../../../assets/fileupload.gif)<!--{: width="714"}-->

Uploaded tables display under the **File Uploads** section of the table list (in both the All Tables and Synced Tables options) in the Data Warehouse Manager:

![](../../../assets/upload-tables.png)<!--{: width="717" height="433"}-->

## Updating or appending data to an existing table {#appending}

Got some new data to add to a file you have already uploaded? No problem - you can easily update and append data in MBI.

1. To get started, go to **Manage Data > File Uploads**.

1. Click the **Edit/Upload CSV to Existing Tables** tab.

1. In the dropdown, click the name of the table you want to update or append.

1. Use the dropdown to select the option for handling duplicate rows:

    `Overwrite old row with new row`|This will overwrite existing data with new data if a row has the same primary key in both the existing table and the new file. This is the method to use for columns with values that change over time - for example, a Status column. Existing data will be overwritten and updated with the new data. Rows with primary keys not in the existing table will be added as new rows.
    `Retain old row; discard new row`|This will cause new data to be ignored if a row has the same primary key in both the existing table and the new file.
    `Purge all existing rows first and ignore duplicate keys within the file`|This will delete any existing data and replace it with the new data from the file. **You should only use this option if you do not need any of the data in the existing table.**

1. Click **Choose File** and select the file.

1. Click **Open** to start the upload.

    After the upload completes, MBI will validate the data structure in the file. A *Success!* message appears at the top of the screen after your table is saved.

## Data availability {#availability}

Just like calculated columns, data from file uploads is available after the next update cycle completes. If an update was in progress during the file upload, the data will not be available until after the next update. Once an update cycle is completed, you can navigate to the Data Preview tab in your data warehouse to ensure that the file uploaded correctly and data is displaying as expected.

## Wrapping up {#wrapup}

This article covered only the basics for using importing data, but we are betting you want to do something a little more advanced. Check out the Related articles for guidance on formatting and importing financial, eCommerce, ad spend, and other types of data.

Additionally, file upload is not the only way to get your data into MBI. The [Data Import API](https://devdocs.magento.com/mbi/docs/import-api.html) allows you to push arbitrary data into your MBI data warehouse.

## Related {#related}

* [Formatting and importing financial data](../../best-practices/format-import-financial-data.md)
* [Importing offline / other ad spend data](../connecting-data/import-offline-ad-data.md)
* [Expected Google ECommerce data](../integrations/google-ecommerce-data.md)

## Third Party Resources

* [Numbers Data Formatting Guide](http://www.dummies.com/how-to/content/how-to-choose-a-number-format-in-your-numbers-spre.html)
* [Google Docs Data Formatting Guide](https://support.google.com/docs/answer/56470?hl=en)

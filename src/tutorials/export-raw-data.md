---
title: Exporting Raw Data
zendesk_id: 360016505532
---

Using raw data exports, you can export records from your Magento BI Data Warehouse to get a closer look at what\'s powering your dashboard. Additionally, raw data exports can help you [pinpoint data discrepancies](https://support.magento.com/hc/en-us/articles/360016730631).

Raw data exports provide access to additional columns and dimensions generated through de-normalization and pre-aggregation of relevant metrics. For example, **User\'s first order date** is a dimension that you can export for each user in Magento BI, while it may not be available in your database.

This tutorial covers the following

* [Selecting Data to Export](#select)
* [Downloading the Export (.csv file)](#download)
* [Accessing Historical Exports](#historical)

## Step 1: Selecting Data to Export {#select}

There are two ways you can export raw data in Magento BI: at the chart level or at the table level.

### Exporting at the Table Level in your Manage Data Tab

If you want to export the table from **Manage Data** tab, you\'ll need [Admin]({% link administrator/user-management/user-management.md %}) permissions.

1. Click **Manage Data** &gt; **Export Data** &gt; **Raw Data Export** to get started.
1. You\'ll see an **Export List** of recently created data exports, if any exist. Click **Add Export** to create a new export.
1. The **New Raw Data Export** dialog will display. Here, you can customize your export by selecting or deselecting columns and filters:

     * **Table** - The **Table** field selects the table that data will be exported from. By default, this will display the table you navigated into.
     * **Export Name** - In this field, enter the name of the export. For example: `Philadelphia - Daily Revenue`.
     * **Available Columns** - This field lists the columns (dimensions) in your database that are available for inclusion in the export. To add a column, click its name.
     * **Selected Columns** - This field lists the columns (dimensions) currently included in the export. To remove a column, click its name.
     * **Filter** - This section lists the filters currently applied to the export. These filters can be changed; new filters can also be added to export a particular dataset.
     * When finished, click the **Export Data** button.

### Exporting at the Chart Level from the Dashboard

1. Click the gear icon in the top right corner of any chart.
1. Select **Raw Export** from the drop-down menu to display the **Raw Export** dialog.
1. Customize the export by choosing the table, columns, and filters to include or exclude. Refer to the previous section for more detailed info on the fields in this module. Note that the table that displays in the **Table** field is, by default, the table that powers the chart.
1. When finished, click the **Export Data** button.

Let\'s take a look at the entire process at the chart level.

![]({% link images/Chart-level_export.gif %})

## Step 2: Downloading the Export {#download}

The export will begin processing immediately after completing your selections in the **Raw Data Export** dialog. As some exports can be large in size, they are limited to 10 million rows and may take some time to run.

To check if your export is ready, click the **Raw Data Exports** button in the top right corner of the screen. Click the **Download** button to download a zipped .csv of your export.

![]({% link images/Downloading_export.gif %})

## Step 3: Accessing Historical Exports {#historical}

To view your past exports, click the **Raw Data Export** button in the top right corner of the screen. Pending and completed reports can be accessed for up to seven days.

## Congratulations! You've finished.

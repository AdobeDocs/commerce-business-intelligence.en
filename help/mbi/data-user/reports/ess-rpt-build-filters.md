---
title: Filters
description: Learn how to use filters.
exl-id: eb683dfe-9a90-400a-a0c0-3dc00d1f28b5
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
---
# Filters

One or more filters can be added to limit the data that is used to product a report. Each filter is an expression that includes a column from the associated table, an operator, and a value. For example to include only repeat customers, you might create a filter that includes only customers who have placed more than one order. Multiple filters can be used with logical `AND/OR` operators to add logic to the report.

>[!TIP]
>
>A report can have a maximum of 3,500 data points. To reduce the number of data points, use a filter to reduce the amount of data that is used to generate the report.

[!DNL Adobe Commerce Intelligence] includes a selection of filters that you can use "out of the box (OOTB)," or modify to suit your needs. There is no limit to the number of filters that you can create.

## To add a filter:

1. In the chart, hover over each data point.

   In this report, each data point shows the total number of customers for the month.

1. In the left panel, click the Filters (![Filter icon](../../assets/magento-bi-btn-filter.png)) icon.

    ![Add Filter](../../assets/magento-bi-report-builder-filter-add.png)

1. Click **[!UICONTROL Add Filter]**.

    Filters are numbered alphabetically, and the first is `[A]`. The first two parts of the filter are dropdown options, and the third part is a value.

      ![Filter interface showing add filter option](../../assets/magento-bi-report-builder-filter-add-a.png)

    * Click the first part of the filter and choose the column that you want to use as the subject of the expression.

        ![Choose First Part of Filter](../../assets/magento-bi-report-builder-filter-part1.png)

    * Click the second part of the filter and choose the operator.

        ![Choose the operator](../../assets/magento-bi-report-builder-filter-part2.png)

    * In the third part of the filter, enter the value that is needed to complete the expression.

        ![Enter the value](../../assets/magento-bi-report-builder-filter-part3.png)

    * When the filter is complete, click **[!UICONTROL Apply]**.

        The report now includes only repeat customers, and the number of customer records retrieved for the report has been reduced from 33,000 to 12,600.

        ![Filtered Report](../../assets/magento-bi-report-builder-filter-report.png)<!--{: .zoom}-->

1. In the sidebar, click the perspective (![Perspective icon](../../assets/magento-bi-btn-perspective.png)) icon.

    ![Perspective](../../assets/magento-bi-report-builder-filter-perspective.png)<!--{: .zoom}-->

1. In the list of settings, choose `Cumulative`. Then, click **[!UICONTROL Apply]**.

    ![Cumulative Perspective](../../assets/magento-bi-report-builder-filter-perspective-cumulative.png)

    The `Cumulative` perspective distributes the change over time, rather than showing the jagged up and downs for each month.

1. Enter a `Title` for the report and click **[!UICONTROL Save]** it as a `Chart` to your dashboard.

    ![Save to Dashboard](../../assets/magento-bi-report-builder-filter-perspective-cumulative-save.png)

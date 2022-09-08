---
title: Tracking Goals Against Actual Metrics
zendesk_id: 360016506172
---

A large majority of our clients often would like to track their **business goals**, but don\'t realize this is possible in Magento BI. In this article, we demonstrate how to set up a dashboard that will help you track your business goals against your actual data - including revenue, new registered users, and orders over time. We\'ll also show you how to compare year over year performance, all in a dashboard like this:

![](../assets/Goals-_dashboard_2.png)

Before getting started, you\'ll want to familiarize yourself with our [file uploader](../data-analyst/importing-data/connecting-data/using-file-uploader.md) and make sure you\'ve defined your business goals for a given period of time.

#### Getting Started

You will need to first upload a file containing specific daily/monthly/quarterly targets for your business.

You can use the [file uploader](../data-analyst/importing-data/connecting-data/using-file-uploader.md) and the image below to format your file. The most common targets that our clients track in Magento BI include Orders, Revenue, and New registered accounts.

![](../assets/Goals-_Excel.png)

#### Metrics

You will need to create one new metric for each target. For example, if you upload monthly revenue and orders targets, you will need to create two new metrics:

* **Monthly revenue target**
* In the <span class="wysiwyg-color-blue">**`Monthly goals`**</span> table
* This metric performs a **Sum**
* On the <span class="wysiwyg-color-blue">**`Revenue target`**</span> column
* Ordered by the <span class="wysiwyg-color-blue">**`Month`**</span> timestamp
{: style="list-style-type: circle;"}

* **Monthly orders target**
* In the <span class="wysiwyg-color-blue">**`Monthly goals`**</span> table
* This metric performs a **Sum**
* On the <span class="wysiwyg-color-blue">**`Orders target`**</span> column
* Ordered by the <span class="wysiwyg-color-blue">**`Month`**</span> timestamp
{: style="list-style-type: circle;"}

* **Monthly new registered accounts target**
* In the <span class="wysiwyg-color-blue">**`Monthly goals`**</span> table
* This metric performs a **Sum**
* On the <span class="wysiwyg-color-blue">**`New registered accounts target`**</span> column
* Ordered by the <span class="wysiwyg-color-blue">**`Month`**</span> timestamp
{: style="list-style-type: circle;"}

#### Reports

As always, it is helpful to have a mix of static values and visual charts when analyzing your targets. Below are three example reports to get you started tracking your revenue performance.

* **Revenue left to achieve target**
* *Metric A: Revenue*
* Metric: Revenue
{: style="list-style-type: square;"}

* *Metric B: Target Revenue*
* Metric: Monthly Revenue Target
{: style="list-style-type: square;"}

* *Formula: Revenue left to achieve target*
* Formula: (B-A)
* Format: Number
{: style="list-style-type: square;"}

* *Time period: (Whatever relevant time period you want)*
* *Interval: Month*
* *Chart Type: Scalar*
{: style="list-style-type: circle;"}

* **Revenue targets**
* *Metric A: Revenue*
* Metric: Revenue
{: style="list-style-type: square;"}

* *Metric B: Target Revenue*
* Metric: Monthly Revenue Target
{: style="list-style-type: square;"}

* *Metric C: Revenue (amount change since previous year)* (hide)
* Metric: Revenue
* Perspective: Amount change vs. Previous year
{: style="list-style-type: square;"}

* *Formula: (This month last year)*
* Formula: (A-C)
* Format: Currency
{: style="list-style-type: square;"}

* Turn "Multiple Y-Axes" off
* *Time period: (Whatever relevant time period you want)*
* *Interval: Month*
* *Chart Type: Line Chart*
{: style="list-style-type: circle;"}

Once you've completed the above reports for revenue targets, you can create identical reports for goals around orders, registered accounts, or any other values you've included in your goals file upload.

After compiling all the reports, you can organize them on the dashboard as you desire. The end result may look like the image at the top of this page.

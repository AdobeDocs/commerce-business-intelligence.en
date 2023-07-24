---
title: Increasing ROI on your advertising campaigns
description: Learn about a few different methods of evaluating your campaign performance.
exl-id: 4f2bf408-eeaf-4dbf-b62e-89426734640a
role: Admin, User
feature: Business Performance
---
# Advertising Campaigns and ROI

[!DNL Adobe Commerce Intelligence] allows you to easily [marry advertising cost data and revenue data](../../data-analyst/importing-data/integrations/google-adwords.md) from your database. This helps you identify which campaigns have the highest return on investment (ROI). This topic explores a few different methods of evaluating your campaign performance.

## Prerequisites

* Import your advertising cost data:
  * [Connect your [!DNL Google AdWords] to [!DNL Commerce Intelligence]](../importing-data/integrations/google-adwords.md): This syncs your [!DNL Adwords] spend in [!DNL Commerce Intelligence]
  * [Upload other advertising cost data](../importing-data/connecting-data/import-offline-ad-data.md): This is recommended for channels without a direct connector to [!DNL Commerce Intelligence]
  * If you import cost data from multiple sources, you can [consolidate](../../best-practices/consolidating-your-tables.md) the data in [!DNL Commerce Intelligence]. Simply [submit a support ticket](../../guide-overview.md#Submitting-a-Support-Ticket).
* [Track user acquisition channel data](../analysis/google-track-user-acq.md)

## User acquisition campaigns

Campaigns targeted at user acquisition can be measured from many perspectives, including:

1. The number of new users acquired of campaigns
1. The conversion rate from registration to purchase of campaigns
1. The ROI of campaigns based on average user lifetime value (LTV)

Analyses (1) and (2) above are explored in a separate tutorial on [identifying your top marketing channels](../analysis/most-value-source-channel.md). Here, you explore analysis (3) to measure campaign ROI over time. This answers whether users acquired from a particular campaign generated enough lifetime revenue to cover the cost of acquisition.

>[!NOTE]
>
>This example assumes that all campaign costs were exclusively used to acquire new users. In reality, your campaign cost is also shared with acquiring unconverted visits, repeat purchasers and such. By assuming that all cost is used to acquire new registered users, the resulting ROI accounts for the worst case scenario (highest cost per acquisition). You can be sure that your actual ROI is higher than your calculation.
>
>Example: Assuming that you spent $20 on a campaign that generated 10 new users and 10 repeat buyers, your actual cost per new user is $1. But, with the assumption that all cost went to acquire new users, the cost per acquisition is $2.

**1. Start by creating a chart that segments your Ad Cost by Campaigns:**

1. Create a [!UICONTROL Metric] that sums your spend over time
1. Go to [!UICONTROL Data > Metrics]
1. Select `Add New Metric` and select the [!DNL `Adwords...`] table that is recording your [!DNL AdWords] cost data.
1. In the metric editor, give your metric a name (for example, [!UICONTROL AdWord Cost])
1. Using the dropdowns, perform a **Sum** on the `adCost` column in the [!DNL Adwords...] table (Change) ordered by the `date` column.
    ![](../../assets/success-add-new-metric.png)<!--="500" height="303"}-->
1.  Click `Back to Metric List` at the top and go to any dashboard.

1. Create a report that segments spend by campaigns
1. In any dashboard, click [!UICONTROL Add Report > Create report]
1. Select the [!UICONTROL Adword Cost] metric that you just created
1. Set the [!UICONTROL Time period] to `All-time`, and [!UICONTROL Interval] to `None`
1. Under the `Group by` tab, add `campaign` as [!UICONTROL grouping field], and click `Add All` in the box.
1. This report shows your all-time [!DNL AdWords] cost by campaigns

**2. Create a report that counts new users by campaigns:**

1. In any dashboard, click **[!UICONTROL Add Report > Create report]**
1. Select the `New users` metric that counts the number of new registered users over time
1. Set the [!UICONTROL Time period] to `All-time`, and [!UICONTROL Interval] to `None`
1. Under the `Group by` tab, add `campaign` as `grouping field`, and click **`Add All`** in the box
1. This report shows your all-time registered users by campaigns

**3. Create a report that segments average user LTV by campaigns:**

1. In any dashboard, click **[!UICONTROL Add Report > Create report]**
1. Select the `Average lifetime revenue` metric that calculates an average user's lifetime revenue
1. Set the [!UICONTROL Time period] to `All-time`, and [!UICONTROL Interval] to `None`
1. Under the `Group by` tab, add `campaign` or `utm\_campaign` as [!UICONTROL grouping field], and click `Add All` in the box 
1. This report shows your average user lifetime revenue by campaigns

**Finally, calculate campaign ROI by bringing together these three analyses in one report:**

1. In any dashboard, click **[!UICONTROL Add Report > Create new report]**
1. Add as input, use the three metrics used above. Each is assigned a letter (for example,\[`A`\], \[`B`\], and \[`C`\])
1. [!UICONTROL Cost]: Add the metric AdWords cost - this is variable \[A\]. This returns cost by campaigns.
1. [!UICONTROL Users]: Add the metric New Users - this is variable \[B\]. This returns the number of users by campaigns.
1. [!UICONTROL LTV]: Add the metric Average Lifetime Revenue - this is variable \[`C`\]. This returns LTV by campaigns.

1. Click the hide icon beside the word Chart so you can focus on the table
1. Now use `Add Formula` to combine these metrics, as follows:
1. [!UICONTROL ROI]: Enter the formula `(\[C\]-\[A\]/\[B\])/(\[A\]/\[B\])`, if \[`A`\] represents `Ad Cost by Campaigns`, \[`B`\] represents `New users by campaigns`, and \[`C`\] `LTV by campaigns`. This returns the ratio of (average user LTV - average cost per acquisition) / (average cost per acquisition)
1. [!UICONTROL Avg Return per User]: Enter the formula **\[`C`\]-(\[`A`\]/\[`B`\])**. This return the average margin made on a user by calculating (average user LTV) - (average cost per acquisition).
1. [!UICONTROL CPA]: Enter the formula **`\[A\]/\[B\]`**. This returns the actual campaign's cost per acquisition.
1. Other potential metrics to include from [!DNL AdWords] data include sums of  `Impressions` and `adClicks` (from [!DNL AdWords] data), along with the total `number of orders` made via a particular campaign.
1. It may also be interesting to calculate the ROI based on LTV 30 days and 90 days after a user registers or makes a first purchase.

1. Feel free to click and drag your metrics and formulas to reorder the columns of your report
1. Name your report and be sure to save as a table.

## Product campaigns

Are you running product-specific advertisements? If so, you can measure ROI on those campaigns by calculating revenue / cost for specific product(s).

>[!NOTE]
>
>This example assumes that all campaign costs were exclusively used to generate purchases of specific product(s). By assuming that all cost was spent on generating purchases, the resulting ROI accounts for the worst case scenario (highest cost per purchase). You can be sure that your actual ROI is higher than this calculation. Example: Assuming that you spent $20 on a campaign that generated 10 new users and 10 purchases, your actual cost per purchase is $1. Under the assumption that all cost went to acquire new users, the cost per purchase is $2.

Before you start, [submit a support ticket](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) to join the following dimensions to your line items table (`sales\_flat\_order\_item, order\_item`):

* Order's source (if you only track referral source at the user level, then join user's source)
* Order's campaign (if you only track referral source at the user level, then join user's campaign)
* Order's medium (if you only track referral source at the user level, then join user's medium)

**1. Now start by creating a chart that returns revenue per campaign for specific product(s):**

1. In any dashboard, click **[!UICONTROL Add Report > Create new report]**
1. Select the `Revenue by items` metric that calculates revenue at the line items level
1. Set the [!UICONTROL Time period] to `All-time`, and [!UICONTROL Interval] to `None`
1. Under the `Filter by` tab, add `product name 'IN'` Product `A`, Product `B`, Product `C`, ..." and include all product names targeted by your campaign separated by a comma (for example, `product name 'IN' yellow t-shirt`, `red t-shirt, blue t-shirt`)
1. Under the `Group by` tab, add `order's campaign` or `order's utm\_campaign` as `grouping` field, and click **[!UICONTROL Add All]** in the box
1. This report shows you the revenue for specific product(s) by campaigns

**2. To calculate ROI, you again combine metrics in one report:**

1. In any dashboard, click **[!UICONTROL Add Report > Create new report]**
1. Add the `Revenue by items` metric, following the filter and group by directions from the campaign for specific product(s) report above and click **[!UICONTROL Hide]** beneath the metric's scalar value
1. Now add the [!DNL AdWords Cost] metric, following the filter and group by directions from the `Ad cost by campaigns` report you explored in the `User acquisition campaigns` section above; then click **[!UICONTROL Hide]** beneath the metric's scalar value
1. With these metrics in place, add formulas:
1. [!UICONTROL ROI]: Enter the formula `\[A\]/\[B\]`, if `\[A\]` represents `Revenue per campaign for specific product(s)` and `\[B\]` represents `Ad cost by campaigns`. This returns the ratio of (Revenue for specific product(s)) / (Campaign Cost)
1. [!UICONTROL Return]: Enter the formula `\[A\]-\[B\]`. This returns the average margin made on a user by calculating (average user LTV) - (average cost per acquisition)
  1. (Optional) [!UICONTROL Revenue]: Unhide the `Revenue by items` metric to see revenue for specific product(s) per campaigns
  1. (Optional) [!UICONTROL Cost]: Unhide the `AdWords Cost` metric to see the cost for campaigns

1. Give your report a name and be sure to save it as a table

**3. Repeat steps 1 and 2 above for each of your advertised product(s) or product group(s).**

## Related documentation

* [Track order referral source via [!DNL Google Analytics] E-Commerce](../importing-data/integrations/google-ecommerce.md)
* [Track user referral source in your database](../analysis/google-track-user-acq.md)
* [Track user device, browser, and OS data in your database](../analysis/track-usr-dev-browser.md)
* [Discover your most valuable acquisition sources and channels](../analysis/most-value-source-channel.md)
* [Connect your [!DNL Google Adwords] account](../importing-data/integrations/google-adwords.md)
* [How does [!DNL Google Analytics] UTM attribution work?](../analysis/utm-attributes.md)
* [Five best practices for UTM tagging in [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)

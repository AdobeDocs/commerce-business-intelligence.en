---
title: Increasing ROI on your advertising campaigns
zendesk_id: 360016732971
---

Magento BI allows you to easily [marry advertising cost data and revenue data]({% link data-analyst/importing-data/integrations/google-adwords.md %}) from your database. This will help you identify which campaigns have the highest ROI. In this article, we\'re going to explore a few different methods of evaluating your campaign performance.

## Prerequisites

* Import your advertising cost data:
  * [Connect your Google AdWords to Magento BI]({% link data-analyst/importing-data/integrations/google-adwords.md %}): This will automatically sync your Adwords spend in Magento BI
  * [Upload other advertising cost data]({% link data-analyst/importing-data/connecting-data/import-offline-ad-data.md %}): This is recommended for channels without a direct connector to Magento BI
  * If you import cost data from multiple sources, we can [consolidate]({% link best-practices/consolidating-your-tables.md %}) the data in Magento BI. Simply [submit a support ticket]({% link getting-started/support.md %}).
* [Track user acquisition channel data]({% link data-analyst/analysis/google-track-user-acq.md %})

## User acquisition campaigns

Campaigns targeted at user acquisition can be measured from many perspectives, including:

1. The number of new users acquired of campaigns
1. The conversion rate from registration to purchase of campaigns
1. The ROI of campaigns based on average user lifetime value (LTV)

Analyses (1) and (2) above are explored in a separate tutorial on [identifying your top marketing channels]({% link data-analyst/analysis/most-value-source-channel.md %}). Here we\'ll explore analysis (3) to measure campaign ROI over time. This will answer whether users acquired from a particular campaign generated enough lifetime revenue to cover his or her cost of acquisition.

Note that we will make the assumption that all campaign costs were exclusively used to acquire new users. In reality, your campaign cost is also shared with acquiring unconverted visits, repeat purchasers, etc. Yet by assuming that all cost is used to acquire new registered users, the resulting ROI will account for the worst case scenario (highest cost per acquisition), so you can be sure that your actual ROI is higher than our calculation.

*(e.g. Assuming that you spent $20 on a campaign that generated 10 new users and 10 repeat buyers, your actual cost per new user is $1, but under our assumption that all cost went to acquire new users, the cost per acquisition is $2.)*

**A. Let\'s start by creating a chart that segments your Ad Cost by Campaigns:**

1. Create a Metric that sums your spend over time
1. Go to Data -&gt; Metrics
1. Select \"Add New Metric\" and select the \"Adwords...\" table that is recording your AdWords cost data.
1. In the metric editor, give your metric a name (e.g. AdWord Cost)
1. Using the drop-down menus, perform \" a \'**Sum**\' on the \'**adCost**\' column in the Adwords... table (Change) ordered by the \'**date**\' column.
    ![2013-10-16\_1247.png]({% link images/2013-10-16_1247.png %}){: width="500" height="303"}
1. We\'re done. Click on \"Back to Metric List\" at the top and go to any dashboard.

1. Create a report that segments spend by campaigns
1. In any dashboard, click Add Report -&gt; Create new report
1. Select the \"Adword Cost\" metric that we just created
1. Set the \"Time period\" to All-time, and \"Interval\" to None
1. Under the \"Group by\" tab, add \"campaign\" as grouping field, and click \"Add All\" in the box below.
1. This report will show your all-time AdWord cost by campaigns

**B. We will then create a report that counts new users by campaigns:**

1. In any dashboard, click Add Report -&gt; Create new report
1. Select the \"New users\" metric that counts the number of new registered users over time
1. Set the \"Time period\" to All-time, and \"Interval\" to None
1. Under the \"Group by\" tab, add \"campaign\" as grouping field, and click \"Add All\" in the box below
1. This report will show your all-time registered users by campaigns

**C. Now let\'s also create a report that segments average user LTV by campaigns:**

1. In any dashboard, click Add Report -&gt; Create new report
1. Select the \"Average lifetime revenue\" metric that calculates an average user\'s lifetime revenue
1. Set the \"Time period\" to All-time, and \"Interval\" to None
1. Under the \"Group by\" tab, add \"campaign\" or \"utm\_campaign\" as grouping field, and click \"Add All\" in the box below
1. This report will show your average user lifetime revenue by campaigns

**Finally we will calculate campaign ROI by bringing together these three analyses in one report:**

1. In any dashboard, click Add Report -&gt; Create new report
1. Add as input we will use the three metrics we used above. Each will be assigned a letter (i.e. \[A\], \[B\], and \[C\])
1. **Cost**\: Add the metric AdWords cost - this will be variable \[A\]. This will simply return cost by campaigns.
1. **Users**\: Add the metric New Users - this will be variable \[B\]. This will simply return the number of users by campaigns.
1. **LTV**\: Add the metric Average Lifetime Revenue - this will be variable \[C\]. This will simply return LTV by campaigns.

1. Click the hide button beside the word Chart so you can focus on the table
1. Now we will use the Add Formula button to combine these metrics, as follows:
1. **ROI**\: Enter the formula **\"(\[C\]-\[A\]/\[B\])/(\[A\]/\[B\])\"**, if \[A\] represents \"Ad Cost by Campaigns\", \[B\] represents \"New users by campaigns\", and \[C\] \"LTV by campaigns\". This will return the ratio of (average user LTV - average cost per acquisition) / (average cost per acquisition)
1. **Avg Return per User**\: Enter the formula **\"\[C\]-(\[A\]/\[B\])\"**. This will return the average margin made on a user by calculating (average user LTV) - (average cost per acquisition).
1. **CPA**\: Enter the formula **\"\[A\]/\[B\]\"**. This will return the actual campaign\'s cost per acquisition.
1. Other potential metrics to include from AdWords data include sums of  *Impressions* and <em>adClicks </em>(from AdWords data), along with the total *number of orders* made via a particular campaign.
1. It may also be interesting to calculate the ROI based on LTV 30 days and 90 days after a user registers or makes a first purchase.

1. Feel free to click and drag your metrics and formulas to reorder the columns of your report
1. Name your report and be sure to save as a table.

## Product campaigns

Are you running product specific advertisements? If so, you can measure ROI on those campaigns by calculating revenue / cost for specific product(s).

Note that we will make the assumption that all campaign costs were exclusively used to generate purchases of specific product(s). By assuming that all cost was spent on generating purchases, the resulting ROI will account for the worst case scenario (highest cost per purchase), so you can be sure that your actual ROI is higher than this calculation.

*(e.g. Assuming that you spent $20 on a campaign that generated 10 new users and 10 purchases, your actual cost per purchase is $1, but under our assumption that all cost went to acquire new users, the cost per purchase is $2.)*

Before we start, [submit a support ticket]({% link getting-started/support.md %}) to join the following dimensions to your line items table (e.g. sales\_flat\_order\_item, order\_item, etc.):
{: style="padding-left: 30px;"}

* Order\'s source (if you only track referral source at the user level, then join user\'s source)
* Order\'s campaign (if you only track referral source at the user level, then join user\'s campaign)
* Order\'s medium (if you only track referral source at the user level, then join user\'s medium)

**A. Now let\'s start by creating a chart that returns revenue per campaign for specific product(s):**

1. In any dashboard, click Add Report -&gt; Create new report
1. Select the \"Revenue by items\" metric that calculates revenue at the line items level
1. Set the \"Time period\" to All-time, and \"Interval\" to None
1. Under the \"Filter by\" tab, add \"product name \'IN\' Product A, Product B, Product C, ...\" and include all product names targeted by your campaign separated by a comma (e.g. \"product name \'IN\' yellow t-shirt, red t-shirt, blue t-shirt\")
1. Under the \"Group by\" tab, add \"order\'s campaign\" or \"order\'s utm\_campaign\" as grouping field, and click \"Add All\" in the box below
1. This report will show you the revenue for specific product(s) by campaigns

**B. To calculate ROI, we will once again combine metrics in one report:**

1. In any dashboard, click Add Report -&gt; Create new report
1. Add the \"Revenue by items\" metric, following the filter and group by directions from the campaign for specific product(s) report above and click \"Hide\" beneath the metric\'s scalar value
1. Now add the \"AdWords Cost\" metric, following the filter and group by directions from the \"Ad cost by campaigns\" report we explored in the \"User acquisition campaigns\" section above; then click \"Hide\" beneath the metric\'s scalar value
1. With these metrics in place, we\'ll now add formulas:
1. **ROI**\: Enter the formula **\"\[A\]/\[B\]\"**, if \[A\] represents \"Revenue per campaign for specific product(s)\" and \[B\] represents \"Ad cost by campaigns\". This will return the ratio of (Revenue for specific product(s)) / (Campaign Cost)
1. **Return**\: Enter the formula **\"\[A\]-\[B\]\"**. This will return the average margin made on a user by calculating (average user LTV) - (average cost per acquisition)
1. (Optional) Revenue: Unhide the \"Revenue by items\" metric to see revenue for specific product(s) per campaigns
1. (Optional) Cost: Unhide the \"AdWords Cost\" metric to see the cost for campaigns

1. Give your report a name and be sure to save it as a table

**C. Repeat steps A and B above for each of your advertised product(s) or product group(s).**

## Related documentation

* [Track order referral source via GA E-Commerce]({% link data-analyst/importing-data/integrations/google-ecommerce.md %})
* [Track user referral source in your database]({% link data-analyst/analysis/google-track-user-acq.md %})
* [Track user device, browser and OS data in your database]({% link data-analyst/analysis/track-usr-dev-browser.md %})
* [Discover your most valuable acquisition sources and channels]({% link data-analyst/analysis/most-value-source-channel.md %})
* [Connect your Google Adwords account]({% link data-analyst/importing-data/integrations/google-adwords.md %})
* [How does Google Analytics UTM attribution work?]({% link data-analyst/analysis/utm-attributes.md %})
* [5 best-practice for UTM tagging in Google Analytics]({% link best-practices/utm-tagging-google.md %})

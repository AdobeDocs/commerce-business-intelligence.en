---
title: Google Analytics - Track User Acquisition Source Data Overview
description: Learn how to segment your data by user acquisition source.
exl-id: 2ce3e4f9-4741-4ada-b822-ec6a5ca94497
---
# Segmentation by user acquisition source

>[!NOTE]
>
>The process below does not support [!DNL GoogleUniversal Analytics].

The ability to segment your data by user acquisition source is critical to effectively managing your marketing plan. Knowing the acquisition source of new users shows which channels yield the top returns, and allows your team to allocate marketing dollars with confidence.

If you are not already tracking user acquisition sources in your database, [!DNL MBI] can help you get started:

## Tracking user acquisition source

We recommend two methods to track referral source data based on your setup:

### (Option 1)  Track order referral source data via [!DNL Google Analytics E-Commerce] (Including [!DNL Shopify] Stores)

If you leverage [!DNL Google Analytics E-Commerce] to track your order and sales data, you can leverage our [!DNL [Google Analytics E-Commerce Connector]](../importing-data/integrations/google-ecommerce.md) to sync each order's referral source data. This will allow you to segment revenue and orders by referral source (for example, `utm_source` or `utm_medium`) and also get a sense of customer acquisition sources via [!DNL MBI] custom dimensions such as `User's first order source`.

>[!NOTE]
>
>For Shopify users**: Turn on [!DNL [Google Analytics E-Commerce] tracking in Shopify](http://docs.shopify.com/manual/settings/general/google-analytics#ecommerce-tracking) before connecting your [!DNL Google Analytics E-Commerce] account to [!DNL MBI].

### (Option 2) Saving [!DNL Google Analytics]' acquisition source data in your database

In this article we will explain how to save [!DNL Google Analytics] acquisition channel information into your own database - namely the `source`, `medium`, `term`, `content`, `campaign`, and `gclid` parameters that were present on a user's first visit to your website. For an explanation of these parameters, check out the [!DNL [Google Analytics] documentation](http://support.google.com/analytics/bin/answer.py?hl=en&answer=1191184). Then, we will explore some of the powerful marketing analyses that can be performed with this information in [!DNL MBI].

#### Why?

If you are just looking at the default [!DNL Google Analytics] conversion and acquisition metrics, you are not getting the whole picture. While seeing the number of conversions from organic search versus paid search is interesting, what can you do with that information? Should you spend more money on paid search? That depends on the value of customers coming from that channel, which is not something Google Analytics provides. 

>[!NOTE]
>
>[!DNL [Google Analytics eCommerce Tracking]](https://developers.google.com/analytics/devguides/collection/gajs/gaTrackingEcommerce) does mitigate this problem by storing transaction data in [!DNL Google Analytics], but this solution does not work for non-eCommerce sites, and certain tools like cohort analysis are not easy to do in the [!DNL Google Analytics] interface.

What if you want to email a follow-up deal to all customers acquired from a certain e-mail campaign? Or integrate acquisition data with your CRM system? This is impossible in [!DNL Google Analytics] - in fact, it is against the Terms of Service for [!DNL Google Analytics] to store any data that identifies an individual.  But that does not mean you cannot store this data yourself.

#### The Method

[!DNL Google Analytics] stores visitor referral information in a cookie called `__utmz`. After this cookie is set (by the [!DNL Google Analytics] tracking code), its contents will be sent with every subsequent request to your domain from that user. So in PHP, for example, you could check out the contents of `$_COOKIE['__utmz']` and you would see a string that looks something like this:

> `100000000.12345678.1.1.utmcsr=google|utmccn=(organic)|utmcmd=organic|utmctr=rj metrics`

There is clearly some acquisition source data encoded into the string, and we tested to confirm that this is the visitor's latest acquisition source and associated campaign data. Now we just need to know how to extract the data. Luckily, Justin Cutroni has previously described how this encoding works, and shared some javascript code to extract the key bits of information.

We took this code and translated it into a [PHP library hosted on github](https://github.com/RJMetrics/referral-grabber-php).   To use the library, `include` a reference to `ReferralGrabber.php` and then call

> `$data = ReferralGrabber::parseGoogleCookie($_COOKIE['__utmz']);`

The returned `$data` array will be a map of the keys `source`, `medium`, `term`, `content`, `campaign`, `gclid` and their respective values.

We recommend adding a new table to your database called, for example, `user_referral`, with the columns like: `id INT PRIMARY KEY, user_id INT NOT NULL, source VARCHAR(255), medium VARCHAR(255), term VARCHAR(255), content VARCHAR(255), campaign VARCHAR(255), gclid VARCHAR(255)`. Whenever a user signs up, grab the referral information and store it to this table.

#### How to use this data

Now that we are saving user acquisition source, how can we use it?

Lets suppose we are using a SQL database and have a `users` table with the following structure:

|ID|EMAIL|JOIN_DATE|ACQ_SOURCE|ACQ_MEDIUM|
|--- |--- |--- |--- |--- |
|1|john@abc.com|2012-01-24|google|organic|
|2|jim@abc.com|2012-01-24|google|cpc|
|3|joe@def.com|2012-01-25|direct|-|
|4|jess@ghi.com|2012-01-26|referral|techcrunch.com|
|5|jen@ghi.net|2012-01-30|other|organic|
|...|...|...|...|...|

For starters, we can count the number of users coming from each referral channel by running the following query against your database:

> `SELECT acq_source, COUNT(id) as user_count FROM users GROUP BY acq_source;`

The result will look something like this:

|ACQ_SOURCE|USER_COUNT|
|--- |--- |
|google|294|
|direct|156|
|referral|55|
|other|16|

This is interesting, but of limited use. What we would really like to know is the growth rate of these numbers over time, the amount of revenue generated by each acquisition source, a [cohort analysis](http://cohortanalysis.com/) of users coming from each source, and the probability that a user from one of these channels will return as a customer in the future. The queries required to do these analyses are complex - which is why we built [!DNL MBI]. Armed with this information we can determine our most profitable acquisition channels and focus our marketing time and money accordingly.

### Related

*   **[Track user device, browser and OS data in your database](https://support.magento.com/hc/en-us/articles/360016732911)**
*   **[Discover your most valuable acquisition sources and channels](../analysis/most-value-source-channel.md)**
*   **[Connect your [!DNL Google Adwords] account](../importing-data/integrations/google-adwords.md)**
*   **[Increase ROI on your advertising campaigns](../analysis/roi-ad-camp.md)**
*   **[How does [!DNL Google Analytics] UTM attribution work?](../analysis/utm-attributes.md)**

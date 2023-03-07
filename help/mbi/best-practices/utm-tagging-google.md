---
title: UTM Tracking in Google Analytics
description: Learn about best practices for UTM tracking (tagging) in Google Analytics.
exl-id: 70bfd855-3b3f-469b-99bc-deb8251904b7
---
# UTM Tracking

`UTM` tracking is a tagging convention for URLs that let you analyze where your users are coming from. If you look on the URLs you click from most marketing email or banner ads, you see UTM tagging. It is those long links that end with things like `utm\_source` and `utm\_medium`.

[!DNL Google Analytics] uses `UTM` tagging to know where your traffic is coming from. Some of this information comes from the [HTTP referrer](https://en.wikipedia.org/wiki/HTTP_referer) but the rest of it you have to supply yourself with `UTM` parameters. When you see `google adwords` or `email marketing`, it means those `UTM` parameters being recorded from the original link click and then stored in users' cookies. From there, [!DNL Google Analytics] uses that data to [attribute interesting behaviors](../data-analyst/analysis/google-track-user-acq.md) on your site. Understanding what those parameters are for helps you understand how best to set up and use UTM tagging.

## Best Practices for UTM Tagging

The following lists the five most important things to remember when setting up your URLs with `UTM` tagging.

### 1. Aim to tag every URL that you can control coming to your site

Every time you ask people to click a link, you should be setting up `UTM` tagging. This includes all your email links (your email service provider likely has a way to automatically tag your URLs), ad links, press articles, blog posts.

### 2. Use a tool to create the URL

`UTM`-tagged URLs can be cumbersome. Instead of trying to type them out longhand, use a tool [like this](https://support.google.com/analytics/answer/1033867?hl=en) to help you. This ensures you are thinking through adding all sensible parameters to the URL, and you get the URL to copy-paste right out of it. To manage social links, tools like [!DNL Hootsuite] include the option to add custom URL parameters to all of your links.

### 3. Make sure you are case sensitive in the parameter values

It is important to remember that the tag `utm\_source=adwords` is a different tag than `utm\_source=Adwords`. Consider making everything lower-case.

### 4. Store the UTM parameter values in your database

Each time a transaction or event happens, you want to evaluate the performance of your marketing activities. You can do this by reading the values of the UTM parameter values from the [[!DNL Google Analytics] cookie into your database](../data-analyst/analysis/google-track-user-acq.md).

### 5. Think about how you name campaigns

In order to track how your marketing efforts are improving over time, you will need to be smart about your naming conventions. Keep it simple and minimize as much as possible. Complicated naming systems are harder to maintain. 

Once you are capturing this data in your database, you can evaluate the performance of your marketing and advertising by more sophisticated analysis including [Customer Lifetime Value](../data-analyst/analysis/ess-expected-ltv.md), [Repeat Purchase Rates](../data-analyst/analysis/repurchase-behavior.md), and [Average Order Value](../data-analyst/analysis/basic-analytics.md).

---
title: UTM Tracking in Google Analytics
description: Learn about best practices for UTM tracking (tagging) in Google Analytics.
exl-id: 70bfd855-3b3f-469b-99bc-deb8251904b7
role: Admin, Developer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
TQID: https://experienceleague.adobe.com/IX5oaIr8tbUUeA3ZrIQNUMnG8ApXMBS1hcpecqFW8kg
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
  - id: beb7a3c1-66ab-4786-b879-7621375b3c40
    internal-label: Email marketing
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
---
# UTM Tracking

`UTM` tracking is a tagging convention for URLs that enable you to analyze where your users are coming from. If you look on the URLs you click from most marketing email or banner ads, you see UTM tagging. It is those long links that end with things like `utm\_source` and `utm\_medium`.

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

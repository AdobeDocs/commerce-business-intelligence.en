---
title: Google Analytics and UTM Attribution
description: Learn about the Google Analytics source attribution process.
exl-id: 48b8a3d3-f1ac-4d3f-8f65-db1245c9ae0a
role: Admin, Data Architect, Data Engineer, User
feature: Business Performance
---
# [!DNL Google Analytics] and UTM Attribution

It is critical to [track user acquisition source](../../data-analyst/analysis/google-track-user-acq.md) to [identify the best performing advertising campaigns](../../data-analyst/analysis/most-value-source-channel.md). This topic explores the [!DNL Google Analytics] source attribution process. In other words, what piece of information is recorded when.

## What is attribution?

`Attribution` is about specifying a referral source of a particular activity. Those activities are typically macro-conversions or micro-conversions, macro being things like **purchases**, micro being things like **registration, email sign-up, blog comment,** and so on.

Ideally, each time a conversion event occurs, a referral source is recorded. But how is the source determined?

The reality is that users often come from many sources before they hit/commit a micro or macro conversion. For example, they may come to the site via organic, then leave, then come via paid search, then leave, then come directly to the site itself. This source tracking information is often provided to the site via UTM parameters, but there are more sophisticated systems out there too. For your purposes, focus on [UTM](https://support.google.com/analytics/answer/1033867?hl=en&ref_topic=1032998).

## How does [!DNL Google Analytics] attribute referral sources via UTM parameters?

When the UTM parameters are specified on the URL, these get parsed out and placed into a [!DNL Google Analytics] [cookie](https://en.wikipedia.org/wiki/HTTP_cookie). If a website does not have [!DNL Google Analytics], there is no point in having UTMs. [!DNL Google Analytics] has rules for how it deals with a user who hits multiple URLs with UTMs during their lifetime (more on that later). Assuming the website is configured to capture UTM parameters into an external database, when a micro or macro conversion happens, whatever is in the [!DNL Google Analytics] cookie at the time of conversion gets replicated to the database.

## First click vs. Last click

### Last click attribution

Last click attribution is the most common attribution model employed by [!DNL Google Analytics]. In this case, the [!DNL Google Analytics] cookie represents the UTM parameters for the most recent source before the conversion event, and this is [recorded in the database](../../data-analyst/analysis/google-track-user-acq.md). The [!DNL Google Analytics] cookie only overwrites the previous UTM parameters if the user clicks on a new URL that contains a new set of UTM parameters.

For example, consider a user who first visits a website via [!DNL Google Analytics] *paid search*, then returns via *organic search*, and finally comes back to the *website directly* or via an *email link* **without UTM parameters** before the conversion event. In this example, the [!DNL Google Analytics] cookie says the user's source is organic, since this represents the last source before the conversion. The *path* of the user before that final conversion event is ignored. If instead the user visited the website from an email link with UTM, then the [!DNL Google Analytics] cookie would say that the source is "email". Therefore, if there are existing UTM parameters in the cookie, and the user comes in via direct, the [!DNL Google Analytics] cookie shows the UTM parameters rather than "direct". 

>[!NOTE]
>
>A specific user's [!DNL Google Analytics] cookie parameters are erased when the cookie [expires](https://developers.google.com/analytics/devguides/collection/analyticsjs/cookie-usage), or when a user clears their cookies in the browser.*

### First click attribution

Some paid attribution tools allow you to capture "the pancake stack" of sources in a user's path. In that situation, in the above example, first click attribution would tell us paid search. Alternatively, some websites implement their own cookies that capture a pancake stack and store the first source into their database.

## How to analyze attribution?

[!DNL Google Analytics] has some robust functionality in their web interface that lets you perform four different attribution models:

1. first click
1. last click
1. linear (divide revenue equally across all the sources in the path)
1. weighted (customized attribution)

Now that you understand what is the attribution model for each micro or macro-conversion, the question becomes "What do you do with the totality of a user's conversions?".  For example, look at the UTMs recorded based on the GA last click logic:

*  User registers under organic
*  User's first purchase under paid search $5.00
*  User's second purchase under email $50.00
*  User's third purchase under organic $10.00

Here is where you ask, "How much revenue did I get from paid search? From email?  From organic?". You could say that the answers are 5, 50, and 10 (whatever the last source was), or you could also say that you attribute all revenue to the first source (all 65 goes to organic). You could also apply some weighted analysis or apply the linear model (that is, roughly 22 each).

## Related documentation

*  [Track order referral source via [!DNL Google Analytics] E-Commerce](../importing-data/integrations/google-ecommerce.md)
*  [Track user referral source in your database](../analysis/google-track-user-acq.md)
*  [Track user device, browser, and OS data in your database](../analysis/google-track-user-acq.md)
*  [Discover your most valuable acquisition sources and channels](../analysis/most-value-source-channel.md)
*  [Connect your [!DNL Google Adwords] account](../importing-data/integrations/google-adwords.md)
*  [Increase ROI on your advertising campaigns](../analysis/roi-ad-camp.md)
*  [Five best practices for UTM tagging in [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)

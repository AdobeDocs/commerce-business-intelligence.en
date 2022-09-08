---
title: How Does Google Analytics UTM Attribution Work?
zendesk_id: 360016733031
---

It is critical to [track user acquisition source](../data-analyst/analysis/google-track-user-acq.md) to [identify the best performing advertising campaigns](../data-analyst/analysis/most-value-source-channel.md). In this tutorial, we are going to explore Google Analytics\'s source attribution process. In other words, what piece of information is recorded when.

## What is attribution?

Attribution is about specifying a referral source of a particular activity. Those activities are typically \"macro-conversions\" or \"micro-conversions\", macro being things like **purchases**, micro being things like **registration, email sign-up, blog comment,** and so on.

Ideally, each time a conversion event occurs, a referral source is recorded. But how is the source determined?

The reality is that users often come from many sources before they hit/commit a micro or macro conversion (for example, they may come to the site via organic, then leave, then come via paid search, then leave, then come directly to the site itself). This source tracking information is often provided to the site via UTM parameters, but there are more sophisticated systems out there too. For our purposes, we will focus on [UTM](https://support.google.com/analytics/answer/1033867?hl=en&ref_topic=1032998).

## How does Google Analytics attribute referral sources via UTM parameters?

When the UTM parameters are specified on the URL, these get parsed out and placed into a Google Analytics (GA) [cookie](https://en.wikipedia.org/wiki/HTTP_cookie). If a website does not have GA, there is no point in having UTMs. GA has rules for how it deals with a user who hits multiple URLs with UTMs in the course of their lifetime (more on that later). Assuming the website is configured to capture UTM parameters into an external database, any time a micro or macro conversion happens, whatever is in the GA cookie at the time of conversion would get replicated to the database.

## First click vs. Last click

### Last click attribution

Last click attribution is the most common attribution model employed by Google Analytics. In this case, the GA cookie represents the UTM parameters for the last, or most recent, source prior to the conversion event, and this is what is [recorded in the database](../data-analyst/analysis/google-track-user-acq.md). Note that the GA cookie only overwrites the previous UTM parameters if the user clicks on a new URL that contains a new set of UTM parameters.

For example, consider a user who first visits a website via *paid search*, then returns via *organic search*, and finally comes back to the *website directly* or via an *email link* **without UTM parameters**{: style="font-size: 1em; line-height: 1.45em;"} before the conversion event. In this example, the GA cookie says the user's source is organic, since this represents the last source prior to the conversion. The *path* of the user prior to that final conversion event is ignored. If instead the user visited the website from an email link with UTM, then the GA cookie would say that the source is \"email\". Therefore, if there are existing UTM parameters in the cookie, and the user comes in via direct, the GA cookie will always show the UTM parameters rather than \"direct\". *(Note: A specific user\'s GA cookie parameters will be erased when the cookie [expires](https://developers.google.com/analytics/devguides/collection/analyticsjs/cookie-usage), or when a user clears his or her cookies in the browser.)*

### First click attribution

Some paid attribution tools will allow you to capture \"the pancake stack\" of sources in a user\'s path. In that situation, in our above example, first click attribution would tell us paid search. Alternatively, a minority of websites implement their own cookies that capture a pancake stack and store the first source into their database.

## How to analyze attribution?

GA has some more robust functionality in their web interface that lets you perform four different attribution models:  first click, last click, linear (divide revenue equally across all the sources in the path), and weighted (customized attribution).

Now that you understand what is the attribution model for each micro or macro-conversion, the question becomes what do you do with the totality of a user\'s conversions?  For example, look at the UTMs recorded based on the GA last click logic:

*  User registers under organic
*  User\'s first purchase under paid search $5.00
*  User\'s second purchase under email $50.00
*  User\'s third purchase under organic $10.00

Here is where you ask: How much revenue did I get from paid search?  From email?  From organic?  You could say the answers are 5, 50 and 10 (that is, whatever the last source was), or you could also say that you attribute all revenue to the first source (that is, all 65 goes to organic). You could also apply some weighted analysis or apply the linear model (that is, roughly 22 each).

## Related documentation

*  [Track order referral source via GA E-Commerce](../data-analyst/importing-data/integrations/google-ecommerce.md)
*  [Track user referral source in your database](../data-analyst/analysis/google-track-user-acq.md)
*  [Track user device, browser and OS data in your database](../data-analyst/analysis/google-track-user-acq.md)
*  [Discover your most valuable acquisition sources and channels](../data-analyst/analysis/most-value-source-channel.md)
*  [Connect your Google Adwords account](../data-analyst/importing-data/integrations/google-adwords.md)
*  [Increase ROI on your advertising campaigns](../data-analyst/analysis/roi-ad-camp.md)
*  [5 best-practice for UTM tagging in Google Analytics](../best-practices/utm-tagging-google.md)

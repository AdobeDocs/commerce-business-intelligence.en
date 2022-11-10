---
title: Recommended Data Dimensions for Segmentation and Filtering
description: Learn about best practices for segmentation and filtering. 
---
# Segmentation and Filtering

Good segmentation is what turns a superficial statistic into a business metric that drives decisions.

Want to know who your most valuable customers are? What your most valuable marketing channels are? Which of your products are moving faster and why? To get to any of these answers, you have to start by segmenting your data.

In this article, we share some critical segments that we often recommend to our customers. We also go into detail on what questions these segments can help you answer. Technically, segments are data columns in your database. In [!DNL MBI], we refer to them as dimensions.

![](../../mbi/assets/mbi-critical-segments.png)


## User Segments

User segments help you understand who your users are and how they behave.

* **Age / Birth Year**: How old are your users? How old are your most active users? It usually makes sense to bucket the values into ranges for more effective analysis.
* **Gender**: Do men and women engage with your website differently?
* **Address**: Where do your users come from? Should you focus your marketing efforts on a particular region? Have your recent advertising campaigns performed as expected in your target regions?
* **Customer acquisition source**\: Do you know what marketing channel your users come from? Did they click on an ad or find you via search? [Segmenting your data by user acquisition source](../data-analyst/analysis/google-track-user-acq.md) is the first step in optimizing your new customer acquisition. Step two is to spend more money in what is working and kill what is not.
* **Registration device**: Did users register via your mobile app or your website? iOS or Android? Is your mobile user base big enough to allocate more resources to develop your mobile product? (If you are not tracking this yet, see this topic [about tracking user device](../data-analyst/analysis/track-usr-dev-browser.md).
* **Referred by**: Who are your top influencers? How many users were directly referred by others?
* **Industry**: If you are a B2B business, in which industries do your users work? Which trade organizations are worth joining?
* **Survey responses**: If you perform customer surveys, use the responses as segments for a deeper level of profiling. You can ask questions that complement what you already know about your users or confirm your guesses.
* **First order amount and product category**: Is there a correlation between a user's first order and future purchasing patterns?

## Orders / Events Segments

Order and event segments help with analyzing user behavior and engagement over time.

* **[!UICONTROL Billing / Shipping Address]**: Where do most of your orders come from? Is there a difference between billing and shipping addresses?
* **[!UICONTROL Status]**: How many of your orders failed to complete? What is the ratio of pending orders in the past seven days?
* **[!UICONTROL Customer acquisition source]**: Beyond tracking user acquisition data at a user level, you can also [track it on an order or event level](../data-analyst/analysis/google-track-user-acq.md). A user that registered via one source may very well continue to access your site via other sources.
* **[!UICONTROL Device]**: Are the number of mobile orders increasing? How much of your revenue is currently generated via mobile purchases? (If you are not tracking this yet, see this topic [about tracking order device data](../data-analyst/analysis/track-usr-dev-browser.md).
* **[!UICONTROL Fulfillment Center]**: Which one of your fulfillment centers is generating the most revenue? If you are analyzing the difference between order time and shipping time, which fulfillment center is most responsive?
* **[!UICONTROL Delivery Carrier]**: Which is the most popular carrier? Which carrier has the least number of returned items?
* **[!UICONTROL Discount / Coupon Codes]**: Are your promotions actually generating extra business? How many extra items did your customers buy in addition to the item on sale? How do coupons affect your average order value? What is your average margin on discounted vs. non-discounted items?
* **[!UICONTROL Satisfaction / Rating]**: How satisfied are your customers with their orders? Are your customers likely to refer business to you?

## Product Segments

Product segments help you make merchandising decisions.

* **[!UICONTROL Merchant / Brand]**: Is one specific brand selling faster than the rest? Which brands are under-performing?
* **[!UICONTROL Type / Category]**: Do different user segments enjoy different types of products? Which product categories generate the most repeat business?
* **[!UICONTROL Discount / Coupon Codes]**: Are promotions hurting sales of non-discounted products? How do coupons affect the perceived value of your products?
* **[!UICONTROL Social Activity]**: Is there a correlation between the buzz generated on social media and the quantity sold for a product?
* **[!UICONTROL Size / Variant]**: What is the ratio of inventory that you need of each variant? Which variants can be sold at discount rates?

If you are interested in merchandising, check out a blog post where we explore [how to use product segments to drive repeat business](../data-analyst/analysis/most-value-source-channel.md).

## Establish Customer Profiles

Segmentation experts may want to move beyond one-dimensional slices and begin establishing real customer profiles. For example, people between ages of 13 and 24 that registered via a mobile device put in a group "Young & Mobile". How does this group's behavior compare to the rest of your user base?

This type of analysis is what marketers at Fortune 1000 companies do all day. Prior to the advent of cloud-based business intelligence platforms like [!DNL MBI], it was largely out of reach for the rest of us. Fortunately, that is no longer the case.

## Tracking New Segments

The first step to segment your metrics by the above dimensions is to make sure that you are tracking this data in your database. If it is not tracked, meet with your tech team and find a way to start tracking this data.

Once we confirm that the data is tracked in your database, [contact our support team](../guide-overview.md) to push the dimensions to your [!DNL MBI] metrics and charts, or simply use our Field Management tool to track these fields in [!DNL MBI].

## Related

* [Optimizing your database for analysis](../best-practices/opt-db-analysis.md)

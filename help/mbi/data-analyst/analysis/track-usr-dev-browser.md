---
title: Google Analytics - Track user device and browser data in your database
description: Learn  how many users are actually logging in via mobile devices and how that affects the lifetime value of those users. 
---
# [!UICONTROL Google Analytics] Tracking

With [!UICONTROL Google Analytics] you can [save referral source information](../analysis/google-track-user-acq.md) to understand where your most valuable users are coming from. In this topic, you will learn about the platform (device, browser, etc.) your users are working on. With this, you will be able to understand how many users are actually logging in via mobile devices and how that affects the lifetime value of those users.

## Saving User Device and Browser Data

Every time a request is made to your website, the user's browser sends a User-Agent string with information about the platform making the request. Here are some examples of the User-Agent string:

1. `Mozilla/5.0 (Macintosh; Intel Mac OS X 10\_8\_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/27.0.1453.116 Safari/537.36`
1. `Mozilla/5.0 (Windows NT 6.1; WOW64; rv:17.0) Gecko/17.0 Firefox/17.0`
1. `Mozilla/5.0 (iPhone; U; CPU iPhone OS 4\_0 like Mac OS X; en-us) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8A293 Safari/6531.22.7`
1.` Mozilla/5.0 (iPad; CPU OS 5\_1 like Mac OS X) AppleWebKit/534.46 (KHTML, like Gecko) Version/5.1 Mobile/9B176 Safari/7534.48.3`
1. `Mozilla/5.0 (Linux; U; Android 2.2; en-us; Nexus One Build/FRF91) AppleWebKit/533.1 (KHTML, like Gecko) Version/4.0 Mobile Safari/533.1`

If you look closely, you see that the string contains information about the user's operating system, browser, and the name of the device they are using (if it has a name). Although User-Agent strings vary widely across platforms and even versions of the same platform, it is generally true that the platform name will exist somewhere within. For example, #1 above is a Mac with the Chrome browser, #2 above is a Windows machine with the Firefox browser, #3 is an iPhone, #4 is an iPad, and #5 is an Android device.

This information can be accessed by your server every time a request is made. In PHP, the User-Agent string is stored in `$_SERVER['HTTP_USER_AGENT']`. In Ruby on Rails, it is stored in `request.env['HTTP_USER_AGENT']`. Other languages and environments will allow you to access it in similar ways.

### When should you record this data?

We recommend you add a new field called `Platform` or `User-Agent` to your `Customers` and `Orders` database tables to store this information whenever a user is created or an order is placed. If you are using a SQL database, this field should be a `VARCHAR(255)`. 

>[!NOTE]
>
>The `User-Agent` string is allowed to be much longer than this, but in practice it rarely exceeds this length.

### How do I parse out the useful segments?

There are a number of libraries out there to help you parse the `User-Agent` string into components like operating system, device, and so on. Refer to the [ua-parser project](https://github.com/tobie/ua-parser) to learn more.

With this new information, you can better understand how users access your site. You can then tailor their experience or create marketing campaigns for certain groups.

## Related

*  [Track order referral source via [!DNL Google Anaytics] E-Commerce](../importing-data/integrations/google-ecommerce.md)
*  [Track user referral source in your database](../analysis/google-track-user-acq.md)
*  [Discover your most valuable acquisition sources and channels](../analysis/most-value-source-channel.md)
*  [Connect your [!DNL Google Adwords] account](../importing-data/integrations/google-adwords.md)
*  [Increase ROI on your advertising campaigns](../analysis/roi-ad-camp.md)
*  [How does [!DNL Google Analytics] UTM attribution work?](../analysis/utm-attributes.md)

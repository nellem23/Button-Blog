---
layout:         post
title:          Universal Deep Links
date:           2015-06-29 12:00:00
summary:        DeepLink Kit 1.1 adds support for Apple's new Universal Links
categories:     opensource
author:         Wes Smith
author_url:     http://twitter.com/ioswes
author_handle:  ioswes
---

<p style="border:solid 1px #ededed; padding:5px; margin-bottom:30px; font-size:0.7em; font-weight:bold;" align="center"><a href="https://github.com/usebutton/deeplinkkit" target="_blank">DeepLink Kit</a> v1.1.0 now supports Apple’s new <a href="https://developer.apple.com/library/prerelease/ios/releasenotes/General/WhatsNewIniOS/Articles/iOS9.html#//apple_ref/doc/uid/TP40016198-DontLinkElementID_2" target="_blank">Universal Links</a></p>

Apple is taking bold steps to protect user privacy in iOS 9 and among the largest changes they’ve made is to the way deep links work.

#### So Long Custom Schemes

Custom URL schemes are being shown the door. Up until iOS 9, if app developers wanted to support deep links they would register custom schemes in their app's info.plist (e.g. `google://`). While this is still possible in iOS 9, Apple is actively discouraging doing so because custom URL schemes have some big disadvantages:

- Any app can claim to handle any scheme
- There's no guarantee that registered schemes don’t collide
- They silently fail when an app is not installed

When a user engages with a deep link, that user, and potentially their data, is sent to another app. Imagine the potential security risk and user experience disconnect if the wrong app opens because it claimed the same scheme.

####Universal Links

How many times have you tapped a link in an email and been directed to Safari when what you really want is to be taken into an app?

Currently, linking into an app from an email, for example, requires some type of redirect through Safari. When the email is sent out, there’s no way to know whether it will be opened from a mobile device or computer. The solution is usually to direct the user to a web browser, examine the device, and redirect them accordingly. On a mobile device, that’s not a great experience for the user.

Apple introduced Universal Links in iOS 9 as the new way to link to deep content within apps. There's no need for custom schemes or ushering users to Safari. Instead, developers can now link their web domain and app allowing iOS to directly open URLs in their apps—completely bypassing Safari. This is a great step forward but, if the app is not installed, users still end up in a degraded web experience.

####It's All About Trust

To enable this seamless opening of web links in an app, developers must first establish a trust relationship between their app and web domain. Apple reads a JSON file hosted on the associated web server with some information about the app and URL paths that will be supported. On the app side, developers need to add an entitlement to their Xcode project that declares the web domains their app will accept links from. This needs to match the domain where the JSON file is hosted.

![associated-domain-example](https://cloud.githubusercontent.com/assets/1057077/8138502/43e847bc-1100-11e5-8df4-8f2f190fcf8c.png)

_At the moment, subdomains need to be added individually. Apple hasn’t provided a way to do this dynamically. I guess you’re out of luck if you have a lot of subdomains._

Once the website and app are associated, developers can start receiving universal links in their apps but, the links won’t be arriving where they did before. Universal links come wrapped in `NSUserActivity` objects and are delivered via the delegate method introduced with [Handoff](https://support.apple.com/en-us/HT204681) in iOS 8 `application:continueUserActivity:restorationHandler:`.

The actual tapped URL can be found in the new `webpageURL` property on `NSUserActivity` objects. Apple didn't add any route matching help so developers still need to take the URL, parse it, and route users to the appropriate content just as before. Basically, Apple drops the URL at the front door and it's up to developers to figure out where to take their user. This can be a messy process.

####It's Easier with DeepLink Kit

The mess goes away with DeepLink Kit, our [popular deep link route matching library](https://github.com/usebutton/deeplinkkit). DeepLink Kit allows developers to register blocks of code along with patterns to be matched against incoming URLs. On match, the library calls the provided block and passes a parsed `DPLDeepLink` object with easy access to route and query parameters and more.

DeepLink Kit is now more useful than ever. With universal links, there's a more compelling reason for developers to implement deep links in their apps. Anywhere a user taps a link (Mail, Twitter, Messages, etc.) and that link is properly associated with an app, the user can be deep linked straight into the app—bypassing Safari. But once the URLs come in, you still need to figure out what to do with them.

With DeepLink Kit, routing URLs is very simple. Create a `DPLDeepLinkRouter`, register some routes (with full regex support available), and forward incoming `NSUserActivity` objects to the router. DeepLink Kit does nearly all of the hard work and developers can spend time focusing on creating great user experiences.

For more information about using DeepLink Kit in your app, [checkout the documentation](https://www.usebutton.com/sdk/deep-links/integration-guide).

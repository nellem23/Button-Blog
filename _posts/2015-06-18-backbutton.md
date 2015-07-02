---
layout:         post
title:          App silos and the back button
date:           2015-06-18 08:45:00
summary:        Apple is embracing deep linking in iOS9. The introduction of a back button and the beginnign of the end for app silos.
categories:     ios design
author:         Max Bulger
author_url:     http://twitter.com/maxbulger
author_handle:  maxbulger
---
Navigating through the App Store and across apps is harder than it should be. As mobile devices are used for more and more tasks, its clear we need a better set of tools to help our apps talk to each other and our users. At WWDC this year, Apple began to acknowledge the problem. Introducing better system-level support for deep linking and a cross-app Search API sent a clear message: the days of “app silos” are numbered. 

The feature most representative of this coming change, ironically, went unmentioned at the conference. Instead, it simply appeared in the first iOS9 beta release: a system-level back button. Innocently tucked into the top-left corner, this button appears in apps when a user has arrived via deep link. It lives in the status bar, and, when tapped, it takes the user back to the originating app. 

<center><img src="/images/posts/backbutton.jpg" /></center>

This change is significant, because it makes every iOS deep link a two-way street. Previously, apps could link out, but any hook to return was up to the receiving app to adopt. Many standards, such as App Links, promoted back button adoption, but it was far from guaranteed. By baking this into the OS, Apple has assuaged a major reservation many app developers had about surfacing outbound deep links. There will now always be a breadcrumb to follow back, regardless of the recipients app’s implementation. This is a strong hint from Apple: embrace your link-enabled, connected future. 

The real motivation for this change is user experience. It takes more than one app to accomplish most tasks, whether they’re small and daily, like meeting a friend, or more significant, like booking a trip. Currently, the chain of app experiences that comprise the majority of user journeys must be forged by the user, in spite of the OS. It should be the opposite: we as software developers and designers are meant to make these experiences more coherent for our customers.

Deep links are one foundational tool to start building a cross-app ecosystem. However, they’re just that— a tool. Similarly, the back button is just one of many cross-app features Apple introduced last week. It’s up to us as product developers to  leverage these features to build better experiences, matching user intent with relevant content and functionality. Discovery and navigation between deep states of app experiences will not be solved by the platforms over night, but we can use emerging features to solve them ourselves. 


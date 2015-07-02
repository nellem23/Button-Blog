---
layout:         post
title:          Introducing DeepLink Kit 1.0
date:           2015-05-15 12:31:19
summary:        DeepLink Kit 1.0 is a splendid block-based way to handle your deep links in iOS.
categories:     opensource
author:         Chris Maddern
author_url:     http://twitter.com/chrismaddern
author_handle:  chrismaddern
author_2:         Wes Smith
author_2_url:     http://twitter.com/ioswes
author_2_handle:  ioswes
---

Today we're releasing v1.0 of our open source library <a href="http://github.com/usebutton/DeepLinkKit" target="_blank">DeepLink Kit</a>. DeepLink Kit is a simple way to add deep links to your app in just a few minutes which will also scale to complex route-matching rules with good seperation of responsibility.

We've been working on DeepLink Kit for a while now (as the iOS DeepLink SDK) & have been really excited by the community response. As of today, we feel that we've reached a good snapshot of stable functionality to cut a v1.0 release.

### Add deep links to your app

At it's simplest, you simply need to create a deep link `router` and give it a block of code to execute when it sees a route.

{% highlight objc %}
#import <DeepLinkKit/DeepLinkKit.h>

- (BOOL)application:(UIApplication *)application
        didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {

  // Create a Deep Link Router
  self.router = [[DPLDeepLinkRouter alloc] init];

  // Add a block for a deep link with the format /log/:message
  self.router[@"/log/:message"] = ^(DPLDeepLink *link) {
  	NSLog(@"%@", link.routeParameters[@"message"]);
  };

  return YES;
}
{% endhighlight %}

You then simply send all incoming deep links to the router.

{% highlight objc %}
- (BOOL)application:(UIApplication *)application
            openURL:(NSURL *)url
  sourceApplication:(NSString *)sourceApplication
         annotation:(id)annotation {

  // Pass the incoming deep link into the DeepLink Kit router
  [self.router handleURL:url withCompletion:NULL];

  return YES;
}
{% endhighlight %}

You now have deep link support.

### More complex deep linking

This is a great basic deep link, but there are lots of more complex things we may want to do.

#### Advanced path filtering

DeepLink Kit supports regex to both constrain and extract components of the path, scheme and host. e.g.

{% highlight objc %}
Rule => "/:entity([a-zA-Z0-9]+)/:instanceid([0-9])/show"

=> /order/123/show [matches]
   path components => { "entity" => "order", "entityid" => 123 }
{% endhighlight %}


#### View Controller Mapping

You can also register a DeepLink Handler class to handle an incoming deep link, this will then provide a view controller through a protocol.

{% highlight objc %}
self.router[@"/:incoming/:path"] = [MyDeepLinkHandler class];
{% endhighlight %}

This is great when you have more complex deep links that you want to seperate responsibility for out to Controllers that know about the functionality in question. You can read more about this in the [full documentation](https://www.usebutton.com/sdk/deep-links/integration-guide).

#### A massive thanks.

Thank you to everybody who has contributed to DeepLink Kit. Your pull requests, feedback and support is greatly appreciated! Extra special thanks to: [Patrick Childers](https://github.com/zimmpatrick), [Dasmer Singh](https://github.com/dasmer), [Aaron Brager](https://github.com/getaaron), [Stan Chang Khin Boon](https://github.com/lxcid), [Vojtěch Bartoš](https://github.com/VojtechBartos), [Bryan Irace](https://twitter.com/irace) & [Orta Therox](https://twitter.com/orta).

#### Try it out today

Go check it out on Github ([here](http://github.com/usebutton/deeplinkkit)) and we'd love to hear what you think.

The Button team


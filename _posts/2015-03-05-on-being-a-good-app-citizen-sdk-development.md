---
layout:         post
title:          On being a good App citizen
date:           2015-03-05 12:31:19
summary:        Building great SDKs is hard. In fact, much harder than building a great app because every component you create can be used in any number of ways that you never considered, in any number of environments and with any number of other dependencies. Add to that the etiquette of being a good guest and you end up with a topic that's definitely worth some codised best-practices! 
categories:     annoucements uber ride
author:         Chris Maddern
author_url:     http://twitter.com/chrismaddern
author_handle:  chrismaddern
---

Building great SDKs is hard. In fact, much harder than building a great app because every component you create can be used in any number of ways that you never considered, in any number of environments and with any number of other dependencies. Add to that the etiquette of being a good guest and you end up with a topic that's definitely worth some codified best-practices! 

This is how we think about building an SDK & some of the best practices that we've adopted.

### Remember you're a guest
The first thing to keep in mind when building an SDK is that <em>you are a guest</em>. When you're a guest, you don't walk into the kitchen, grab a beer, put your feet up on the table and change the TV channel (I hope.) You behave in a way that is respectful & doesn't interfere with the normal operations & their enjoyment of their home. The same thing is true when being an SDK inside of somebody's app; but the resources in question aren't beers & televisions, they're networking & permissions, background time & appearance. 

#### Network, Resources & Battery
Use them sparingly. As is eqtiquette in any limited-resource situation; thoughtfulness on the use of resources is expected and appreciated. 

- Batch your network requests which aren't time sensitive. 
- Don't create 'noisy' protocols. 
- Build assets that are pre-sized vs. resizing in the client. 
- Caching is okay, but implement low memory warning behavior to invalidate any optimistic caching. 

#### Style & appearance
Each app has a distinct visual style and appearance attributes. There's a constant trade-off between making something that's consistent with your brand (& effective at solving the problem you're solving), and consistency with the brand of the app that's integrating with your tools. Our sound bite on this is `at home in X, but distinctly Button`. Some of the best-practices that we've adopted here include:

- Clearly decide & state what is customizable & what is not
- Use the UIAppearance Protocol to both configure system-wide appearance and capture any appearance that the app has
- Fonts & colors should usually be customizable

#### Notification & Locations Permissions
This is a really important one. In iOS, apps only get the opportunity to request permissions once & in Android they have to be added to the global list of permissions for that app (potentially discouraging new users). Our rules around permissions are as follows:

- Use them only when you need them (no random data capture)
- Where the app already has the permission in question, use it freely

When you are going to request a permission on behalf of an app:

- Always guard your request with a custom UI component which asks the user first, then shows the system dialog if they confirm
- For any permission you are going to request, have a flag on your SDK which determines whether or not it's allowed to request the permission. This way developers are explicitly in control of their permissions.
- Explain <em>why</em>. This is for both the developer & the user; let them know why you're asking for the permission. They're not only more likely to tap yes, but also understand the need for your SDK to have the permission.

Permissions can be a particularly sensitive area to integrators so make sure not only to follow best practices, but to communicate that you follow these best practices, so that integrators are truly in-control.

### Experience

In order to become a part of an app's user experience, you don't need to be 'as good' - you need to be better. Your UI, flow & experience will come under more scrutiny than they would put their own under & it needs to stand up to that scrutiny. That's right -- you need to deal with all of restrictions outlined in this post, but still build something *amazing*.

This is probably a whole seperate post.

### Build in Layers

As with any problem in computer science, it's best solved by breaking it down into layers which can be built on top of each other. This is definitely true of an SDK.

One discussion we have a lot at Button is 'magic vs. maintainability' (a whole other post here again!) which is the tradeoff between 'magical' two-line integrations and sensible, idiomatic interfaces which actually drive developer understanding of what they're doing (and are internally maintainable and enjoyable to work with). Our solution to this has been to build in layers.

At the bottom, there's a `core` layer which handles all of the mundane SDK setup, managing network resources, authentication etc.. 

On top of that, there are a robust set of idiomatic interfaces to interacting with Button functionality. These are our internal APIs, aggressively tested and meticulously designed.

Then, at the top are magical 'Dropins' which allow the two-line integrations. These sometimes break a few rules in order to achieve really low-friction integrations. They are totally subclass-able to be able to customize functionality but also replaceable -- if the dropin integration isn't right for you, you have the same tools that we had to build your own UI on top of it.

This makes building and maintaining the SDK enjoyable, while also giving really easy paths to integration.

### Testing & Quality
Do it. Your tenancy in an app is over the moment you start crashing & get in the way of their business. Quality at every step of the way is so important.

For more on quality & best practices check out <a href="http://building.usebutton.com/process/best-practices/new-project/2014/10/15/from-file-new-project-to-best-practices/">From File->New Project to Best Practices</a>.

### Semantic Versioning
Version <a href="http://semver.org/">Semantically</a>.

Unintended updates with breaking changes are one of the biggest causes of issues in dependencies. Make sure to version semantically & in all examples & sample code include your library using a defined major version number. e.g. `~> 3.0`. 

### Privacy
App makers (correctly	so) take the privacy of their users and data very seriously. By incorporating your technology into their app, they are sharing this responsibility with you. It is important to both behave responsibly & have a stated policy of what you collect & how it is used.

- Do not collect data that you don't need in the operation of your product
- Do not collect data that you haven't explicitly told the app developer you are collecting
- Have a clearly defined privacy policy and path to data deletion

### Some Housekeeping

There are also some smaller items that are worth noting.

- Avoid logging debug or large amounts of data to the standard output
- Do not use asserts. Never cause a crash.
- Have some way to silently fail / disable your functionality
- Do not show error / background modal views

This is by no means exhaustive, but represents some of the things that we spend a lot of time thinking about with respect to building great SDKs. Let us know what you think is important in SDK building on twitter <a href="http://twitter.com/button">@button</a>.


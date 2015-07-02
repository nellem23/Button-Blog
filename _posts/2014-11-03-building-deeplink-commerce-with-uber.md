---
layout:         post
title:          Launching DeepLink Commerce with Uber
date:           2014-11-03 12:31:19
summary:        How we approached building from the ground up with best-practices in mind even when you're starting with a blank project & potentially only one contributor. 
categories:     annoucements uber ride
author:         Chris Maddern
author_url:     http://twitter.com/chrismaddern
author_handle:  chrismaddern
---

Today we announced the launch of DeepLink Commerce with Uber as our first partner. With the Button SDK and our DeepLink Commerce Uber integration, you can integrate the Uber Ride Picker and Ride Alerts into an App with just a few lines of code. 

Our first integration is live today -- <a href="https://itunes.apple.com/us/app/resy/id866163372?mt=8">Resy</a> was completed in under 4 hours and they're live in the store just days later. It really has never been so easy to create such a rich cross-app experience.

We wanted to use Building Button to share a little bit more about the thought & work that went into building out DeepLink Commerce & creating a seamless user experience. Here's how we did it...
<img src="/images/posts/uber-ride-picker-1.png" class="image-right" />


### Creating a rich integration

We knew going into this that we wouldn't be satisfied with tapping a button and sending the user out to a mobile website; we wanted to create a full App-to-App experience. For partners who integrate with Uber using DeepLink Commerce, we want it to feel like a natural extension of the product that delivers real value and looks, & feels great.

#### At home in Resy, but distinctly Button... and Uber

We have a saying at Button for the work we do in our SDKs.

<blockquote>
"At home in the partner, but distinctly Button."
</blockquote>

This piece of work required a step further... <em>At home in the partner, but distinctly Button.. and Uber</em>. We began with the Button SDK which is designed to provide simple, easy-to-use drop-in controls making beautiful use of blur and animation. These controls are also highly configurable to match the styling of the partner application.

Next, we started to apply the <a href="https://developer.uber.com/v1/design-guidelines/">Uber Brand & Style guidelines</a>. Uber have done an excellent job of providing thorough and concise descriptions of the key aspects of the interface that they have either recommendations or requirements around. Most of the requirements are just good product design & respectful treatment of the brand, other recommendations have come from years of optimizing the process of introducing the concept of 'rides on demand' and getting users to that first, second or hundredth ride. We wanted to listen to that.

#### We'll write 1,000 lines to save you 10

After building an amazing experience, our second objective was to make sure that creating this integration is extremely easy for our partners.

When you're building an SDK, there are dozens of times a day where there's a choice to be made -- one direction puts a small amount of work on the partner while saving you a lot of time. The other direction means investing hours or even days in making sure that every potential situation that the SDK can be used in is considered & handled in your 'magic' in-SDK implementation. The where, when & how of 'magic' in SDKs is another topic that is worth an entire blogpost, but when carefully considered & executed it can produce amazing results.

The integration to display the Uber Ride Picker and trigger a ride (complete with <em>AttendedInstall</em>) from your currentLocation to a given location is two simple lines. These two lines...

{% highlight objc %}
// Create a BTNRideAppAction
BTNRideAppAction *appAction = [BTNRideAppAction rideAppActionWithStartLocation:[BTNRideLocation currentLocation] 
                                                                   endLocation:[BTNRideLocation locationNotFarFromHere]];

// Execute the App Action
[appAction performActionWithCompletion:NULL];
{% endhighlight %}

#### Bring it in-App

We've noticed a couple of things about most App-to-App integrations:

- They're mostly not really App-to-App, more App-to-Web-to-App, or App-to-Web-to-Store-to-App etc..
- They're about moving you, not your intent

That second concept is really important to us. The only way that this integration is <b><em>for the user</em></b>, is if you begin an action in the App with context & that context carries through to the second App.

This led us to the development of <em>AttendedInstall</em>. <em>AttendedInstall</em> allows you to install Uber from within an app & seamlessly send the user (complete with context) across to Uber as soon as it's installed.

<center><img src="/images/posts/install.png" style="max-width:300px;"/></center>

#### Interested in integrating?

We're currently in private beta, but would love to hear from you if you're interested in integrating a highly productised, simple way to get a ride into your app.

<a href="mailto:info@usebutton.com">Get in touch</a>


---
layout:         post
title:          From File→New Project to Best Practices
date:           2014-10-15 12:31:19
summary:        How we approached building from the ground up with best-practices in mind even when you're starting with a blank project & potentially only one contributor. 
categories:     process best-practices new-project
author:         Chris Maddern
author_url:     http://twitter.com/chrismaddern
author_handle:  chrismaddern
---

Starting new projects is fun.. everything will be different this time. There won't be any technical debt, everything will be tested and onboarding new team members to the codebase will be a cinch.

#### But it doesn't quite work like that

You tried that last time... remember? Every commit has a note to add tests for XYZ (or maybe no comments at all), gradually coverage tends towards 0 and you're maintaining a mess.

#### Decide to do great work

The most important component to approaching a new project and creating something which is stable, maintainable and pleasurable to work on is to think ahead of time about doing it & decide that you will.

There are two really hard components to great engineering:

- Committing to doing it
- Actually knowing what consititutes good engineering

Fortunately, the first component can largely lead you towards the second. If you're commited to approaching the product with good engineering best-practices, you can learn these as you go, erring on the side of caution where relevant.

### Declare some policies ahead of time

In order to keep yourself honest, even as you hurtle towards product release dates and have nobody to push back on compromises & cut corners, decide on some policies and write them down.

Ours loosely broke out into the following categories:

#### Test

Tests sometimes seem like they take a lot of time to write & make even simple tasks take a long time. I've always found that the trade-off it creates is that the 20% of the work at the end that takes ~80% of the time, only takes 50% of the time when you have good tests in place.

Set up a test-runner and commit to a testing strategy; then be strict on yourself. For building out the clients at Button, our plan looked something like this:

- 100% code coverage for business logic
- Be sensible about testing views
- Black-box test API functionality

More interesting thoughts on testing: <a href="http://robots.thoughtbot.com/test-driving-ios-a-primer" target="_blank">iOS Testing by Thoughtbot</a>, <a href="http://www.vogella.com/tutorials/AndroidTesting/article.html">Vogella's *extensive* guide to Android Unit Testing</a>... & many, many more!

If you're interested in test methodology, I highly recommend <a href="http://martinfowler.com/articles/mocksArentStubs.html" target="_blank">Mocks aren't stubs</a> by Martin Fowler.. a ripe topic for bar fights between engineers.

#### Pull Requests

Pull requests are a great tool to look at a chunk of work with a critical eye. In a startup, you're forced to wear many hats & this is an opportunity to take off the "let's get this committed and pushed" hat & put on the "is this making the codebase better" hat.

Sometimes it feels a little bit like this...
<blockquote>
  <p>
    <b>Chris</b><br />
    Can I merge this?<br />
    <b>Chris</b><br />
    Sure thing, Chris.
  </p>
</blockquote>

...but Pull Requests are a useful tool, even for small teams or where you don't have a seperate reviewer. 

We tried to be disciplined about breaking functionality up into distinct units (on a branch) and then merging it to master through a P/R. Having an engineer from another discipline or who's totally unfamiliar with the code review it is still extremely valuable in that it allows you to explain your approach & apply fresh eyes to the logic. As a last resort, if you're going to be reviewing your own P/R, try to take a break between finishing the work & reviewing it... or at least do something else for a while.

This allowed us to keep to the overarching principle of <b>keep master clean, building & with the tests passing</b>.

Establishing cross-domain Pull Request reviews was a massive win for us & I'd highly recommend it; as well as increasing reviewers available & speed of review, it also increased exposure to the full stack for the whole team.

On the topic of Pull Requests.. Jeff Kunkle's <a href="http://kunkle.org/blog/2013/07/10/pull-request-etiquette/" target="_blank">Pull Request Etiquette</a> is a good read.

#### Pretend you have users

Developing practices that won't scale to a production that's actually *production* will eventually hurt you. Pretend that you have users from the beginning, keep your environments up & work on deploying in a way which will be able to support your SLAs once you go live. 

Doing this will allow you to <b>put work behind you which you can build on top of</b>, this will accelerate <b>progress</b>.


#### Track your work

This one seems obvious, but it's amazing how many small teams don't track anything. We found that tracking at a level of granularity where an item was <= 1 day of effort made us feel like we were making progress & we had thought about the problem enough to break it up that there weren't too many surprises.

<img src="/images/posts/trello.png" />

We love <a href="http://www.trello.com" target="_blank">Trello</a> for small teams.

#### Deliver Internally

'Delivering' product is the most valuable tool that I've found to measure progress, keep us focussed, encouraged and show the people we're working with what's going on.

Ideally, deliver weekly and share with everybody the `new hotness`. This keeps you working towards milestones and gives you cool things to show off. This will eventually evolve into agile 'demos' once the team grows.

<a href="http://www.hockeyapp.net" target="_blank">HockeyApp</a> is great for sharing mobile application builds & <a href="http://www.flinto.com" target="_blank">Flinto</a> has been great for sharing our design work in a way that's easily understood and interacted with. We use a modified version of <a href="https://github.com/venmo/DryDock-iOS" target="_blank">DryDock</a> which I worked on at Venmo to distribute builds.

#### Document things!

Everything that you want to commit to, write it down. It will help you solidify the decision as well as have a reference to look back at.

#### Continuous Integration

You're writing tests and running them before you push, but crazy things happen in the world of branch merging and Travis CI's P/R test status is a great tool & constant reminder that merging is conditional on tests passing.

<img src="/images/posts/travis_pr.png" />

There's a lot of great tips & code snippets on setting up CI using Travis CI on the <a href="http://www.objc.io/issue-6/travis-ci.html" target="_blank">objc.io post</a>.

#### Imagine you're going to open-source everything...

..and hopefully actually open-source some things. The open-source mindset of documentation, clarity, testing & pride in quality (or ego ;)) will serve you well. Where you build components that are broadly useful but complex, open-sourcing can often be a massive benefit in that the community will maintain it if it's valuable. (Think API wrappers, interfaces, frameworks etc.. especially where any dependencies are subject to regular change.)

#### This sounds like a lot of work

There are two types of work here.. one is upfront & the other is continuous.

The upfront work should be achievable in less than a day (if it isn't this time, it will be next time) and will allow your effectiveness to be multiplied.

The continuous work is a constant investment in the idea that the net win is always to be had with best-practices; if not, why would they be called best-practices? Spend an extra 20% of time upfront on each module & realise massive savings the first time you need to slightly refactor, or encounter an issue; not to mention the reduced risk of production issues.

### Time to scale

Now you want to add more people to the team, time to evolve the process.

The document you created becomes your <b>team charter</b> which can evolve as you need. We use GitHub for this so that you can raise issues and P/Rs.

The weekly deliveries become <b>agile demos</b> and the internal deliveries become the candidates for <b>releasing externally</b>.

Your process for creating tasks in whatever tool you use becomes your <b>sprint planning meeting</b>.

We have found that these practices help us to easily expand the team as we grow & provide a good trade-off that sees us moving quickly while having codebases & a product that we're proud of and enjoy maintaining.

What's worked for you? Let us know on Twitter <a href="http://twitter.com/button">@button</a>
---
layout: single
title: "Cross Browser Testing Reloaded"
excerpt: "How can you perform cross device testing, when the most popular device only accounts for 5% of your traffic?"
comments: false
author_profile: true
categories:
    - Software 
    - Testing
header:
    overlay_color: "#000"
    overlay_filter: "0.6"
    overlay_image: /images/browsersync-sizzy-banner.jpg
    teaser: images/browsersync-sizzy-teaser.jpg
---

We've had a big problem at [U Account][uaccount] for a while now. Our analytics tell us that over 70% of our traffic is mobile, but that traffic is distributed across over 400 devices, with the most popular device only accounting for 5% of that traffic. This leaves us at a bit of a loss as to how we can possibly support that many devices, and how to choose which ones we should support!

[In 2015 OpenSignal were having a similar problem, and put together a brilliant report on this subject][open-signal].

This problem has spawned two main questions for us to answer:

 * How do we decide which devices to support?
 * How do we perform cross-browser testing more efficiently, so that we can cover more ground in the time we've got?

The first question has proven almost impossible to answer thus far, so today I'm going to describe how we've gone about attempting to answer the second question.

## BrowserSync, Physical Devices & Sizzy ##

Our current chosen method of cross-device testing, is a combination of [BrowserSync][browsersync] and [Sizzy][sizzy]. We proxy one of our test platforms through browsersync, using the proxy option:

	$ browser-sync start --http --proxy https://www.uaccount.uk
	[Browsersync] Proxying: https://www.uaccount.uk
	[Browsersync] Access URLs:
	 ---------------------------------------
	       Local: https://localhost:3000
	    External: https://192.168.60.101:3000
	 ---------------------------------------
	          UI: https://localhost:3001
	 UI External: https://192.168.60.101:3001
	 ---------------------------------------

We then point a physical mobile device (or several) and Sizzy at this proxy. BrowserSync then synchronises any interaction with one device across all devices, which means we can test the physical interaction on one device, while seeing how the page looks on many devices at once! We can easily switch to physically interact with any connected device at any time, meaning we could log in on one device, then switch to another to continue testing.

Not a "perfect" solution (is there such a thing?) &mdash; but it's working for us, for now.

<figure>
	<a href="/images/browsersync-sizzy-full.jpg">
		<img src="/images/browsersync-sizzy-full.jpg">
	</a>
</figure>

There are however, a couple of gotchas...

## X-Frame-Options ##

Most semi-security conscious people will have X-Frame-Options set to deny in their http headers. You may need to change the settings with this to allow Sizzy to connect to your test environment. _Don't have this set to allow on a production system!_

## 3rd Party Hosted Fonts ##

Some paid for font services only allow their fonts to be loaded from pre-defined URLs; certainly not on an internal IP, meaning that these fonts won't load if you're proxying through BrowserSync. I don't have a fix for this yet, unless anyone can suggest one?

Enjoy!

  [uaccount]: https://www.uaccount.uk/
  [open-signal]: https://opensignal.com/reports/2015/08/android-fragmentation/
  [browsersync]: https://www.browsersync.io/
  [sizzy]: https://sizzy.co/

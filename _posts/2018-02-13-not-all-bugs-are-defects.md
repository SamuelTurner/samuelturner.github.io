---
layout: single
title: "Not all bugs are defects"
excerpt: "Often testers find issues with software that are not defects, but still don't feel right... so are they bugs?"
comments: false
author_profile: true
categories:
    - Software
    - Testing
header:
    overlay_color: "#000"
    overlay_filter: "0.5"
    overlay_image: /images/software-testing-banner.jpg
    teaser: images/software-testing-teaser.jpg
---

As software testers we often come across aspects of a piece of software that might not necessarily be defects, but they still don't feel right. It may be an intended feature that sounded great on paper &mdash; or in the mind of the stakeholder writing the requirement &mdash; but now we're testing it in context, it feels like a bug.

I once met a wise old tester on my travels who went by the name of [Stephenus Bloweronius][blower-twitter] 4th century BC, who growled out from under the brim of his fedora something which has stuck with me ever since:

> A bug is anything that bugs you, my lad!

If I identify something about a piece of software that I wouldn't be happy leaving in when the software is shipped, I've always raised it and tried to get it fixed. This can be tricky at times, especially when I'm trying to get a stakeholder to revise a requirement.

## Case in point&hellip; ##

I recently came across such a dilemma with my bluetooth headphones. (Which I've [posted about recently already][headphone-post]).

The headphones have an adjustable volume, however that's just for the sound you're transmitting into the headphones. The other sounds it plays (connection established, connection lost and battery low warning) are delivered at at least 150db over the top of the music. While these sounds are annoying in themselves, the real bug lies within the logic that delivers the low battery warning.

When the battery is low, the klaxon sounds, and continues to sound every 30 seconds. *Even if you plug them in to charge.*

This simple feature, reminding the user that their headphones are about run out of electricity, effectively renders them useless until they're charged again. The only option I've found is to turn them off for 20 mins so they can charge enough for the klaxon to stop.

You could interpret this as a missing requirement &mdash; plugging the heaphones in should switch off the klaxon. You could also interpret it a misunderstood requirement &mdash; the sound only needs to alert the user, it doesn't have to make them jump out of their skin. The conclusion however remains the same. It really, really bugs me.

## </rant> ##

Bugs can often be tricky to describe, but it gets a lot easier if you keep them in context. I often see bug reports which try to describe them without mentioning **who** they impact, which makes it very difficult to describe **how** they impact users. Sticking to the format of "If a customer performs an action, an event occurs, and the impact is thus". This format avoids describing a defect, and instead describes an action, a result, and an impact. This way it doesn't matter if it is considered a bug, an updated requirement or an entirely new requirement &mdash; we focus on the impact, leaving decision makers free to choose whether to change it now, later or not at all.

[headphone-post]: {{ site.baseurl }}{% post_url 2018-01-29-fixing-bluetooth-headphones-in-ubuntu-16.04 %}
[blower-twitter]: https://twitter.com/badbud65

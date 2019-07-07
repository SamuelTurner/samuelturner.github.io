---
layout: post
title: "Altered CSS Search Tool"
excerpt: "Script to compare a git branch with a base branch, find the changed/added/removed CSS classes, and search the codebase for uses"
background: /images/ruby-banner.jpg
---

I came across a bit of an issue at work recently - if some CSS in a large codebase gets altered as part of ongoing development, how can we find out what the affect on the website may be? How do we know where the classes are being used?

It's possible to get a list of classes from `git log`, then pass those into [Element Finder][element-finder] to search the codebase for uses of those selectors.

[The script can be viewed here][script].

  [element-finder]: https://github.com/keeganstreet/element-finder
  [script]: https://gist.github.com/SamuelTurner/d79822fb79cd30a678630f831e3ea308
  

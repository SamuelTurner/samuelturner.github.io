---
layout: post
title: "Simple Ruby script for minifying JavaScript"
excerpt: "A simple ruby script I wrote for combining and minifying JavaScript files"
background: /images/ruby-banner.jpg
---

Recently I’ve been getting frustrated by overly complicated tools for
minifying JS but that don’t seem to work properly, so I wrote one.

So far I’ve tried all the popular tools, and either couldn’t get them to
run on Windows easily or thought they were just complicated for my tiny
brain to understand. I just wanted something to pull all of my files
together, remove comments, reduce whitespace and output a single JS
file.

I had a spare day today so I decided to see how simply I could solve the
problem. Turns out that actually it’s very simple indeed, as I’ve ended
up with a single-file Ruby script that is 29 lines long (excluding blank
lines and comments).

Update
------

I decided to pass the combined JS off to an API to minify it instead of
trying to fix the issues I was having with gsubing the bits I didn’t
want.

[View the source of SimpleJSMinifier on Github].

  [View the source of SimpleJSMinifier on Github]: https://github.com/SamuelTurner/SimpleJSMinifier

---
title: Show Only Top-Level OP Comments in Reddit
layout: post
description: Development related tips and tricks from an experienced developer.
date: 2023-11-08 13:51 -0800
categories:
- web
---

If you use Reddit mainly for news, blocking comments can be useful for focus.  However, top-level comments by the author (OP) often have useful context and information.

While logged out of Reddit, using [UBlock Origin](https://ublockorigin.com/){:target="_blank"}, add the following to the `My Filters` tab in settings:

{% highlight css %}
www.reddit.com##div[slot="commentMeta"]:not(:has(shreddit-comment-author-modifier-icon[op="true"])):upward(1)
{% endhighlight %}

*More info: [UBlock Wiki - Procedural cosmetic filters](https://github.com/gorhill/uBlock/wiki/Procedural-cosmetic-filters){:target="_blank"}*

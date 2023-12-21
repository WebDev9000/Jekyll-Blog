---
layout: post
title: Checkout a Github Pull Request without Github CLI
date: 2023-12-11 15:53 -0800
description: Development related tips and tricks from an experienced developer.
categories:
- git
---

Any github Pull Request (PR) can be used locally, even before it's been accepted.  Simply copy the #ID after the PR title, or from the URL: /pull/ID.

From the repo's folder:

{% highlight powershell %}
git fetch origin pull/ID/head:NAME
git checkout NAME
{% endhighlight %}

For example:

{% highlight powershell %}
git fetch origin pull/123/head:123 && git checkout 123
{% endhighlight %}
*More info: [Checking out pull requests locally](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/reviewing-changes-in-pull-requests/checking-out-pull-requests-locally)*

<br />

You can make this a convenient alias. For example, with Powershell:

{% highlight powershell %}
git config --global `
alias.pr '!git fetch origin pull/"$1"/head:"$1" && git checkout "$1" #'

git pr 123
{% endhighlight %}


*Source: [Tom Hale - Git alias with positional parameters](https://stackoverflow.com/a/39523506)*
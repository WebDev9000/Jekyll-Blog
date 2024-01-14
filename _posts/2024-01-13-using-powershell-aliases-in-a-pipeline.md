---
layout: post
title: Using Powershell Aliases in a Pipeline
date: 2024-01-13 16:30 -0800
description: Development related tips and tricks from an experienced developer.
categories:
- cli
- powershell
---

#### Example
To use the alias `m` to launch the editor [Micro](https://github.com/zyedidia/micro){:target="_blank"}, open your Powershell profile in your editor:

{% highlight powershell %}
code $PROFILE
# Or use micro / vim / notepad / etc.
{% endhighlight %}
<br />
Next, add the following function and alias:

{% highlight powershell %}
function _m {$input | micro $args}
Set-Alias -Name m -Value _m
{% endhighlight %}

Note the use of the special variables `$input` and `$args`.

`$input |` allows Micro to respond to information piped to it, such as `echo "test" | m`.

`$args` allows Micro to receieve arguments such as `m --version`

#### More info:

*[about Automatic Variables](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_automatic_variables?view=powershell-7.4){:target="_blank"}*

*[Create a Permanent Powershell Alias from the Command-Line](/cli/powershell/2023/12/31/create-a-permanent-powershell-alias-from-the-command-line.html)*
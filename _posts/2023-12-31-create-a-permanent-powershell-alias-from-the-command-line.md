---
layout: post
title: Create a Permanent Powershell Alias from the Command-Line
date: 2023-12-31 22:07 -0800
description: Development related tips and tricks from an experienced developer.
categories:
---

First, open your Powershell profile in your editor:

{% highlight powershell %}
code $PROFILE
# Or use micro / vim / notepad / etc.
{% endhighlight %}

<br />
Next, add the following function and alias:

{% highlight powershell %}
function _alias {
	Add-Content -Path $PROFILE -Value ""
	Add-Content -Path $PROFILE -Value "function _$($args[0]) {$($args[1])}"
	Add-Content -Path $PROFILE -Value "Set-Alias -Name $($args[0]) -Value _$($args[0])"
}
Set-Alias -Name alias -Value _alias
{% endhighlight %}

Run ```. $PROFILE``` (*remember the dot*) to reload your profile.

<br />
Now simply add new aliases with:

{% highlight powershell %}
alias alias-name 'command(s)-to-run "$args"' && . $PROFILE # to load the new alias
# $args is optional but will pass anything after the alias through to the command.
# Note the use of single quotes.
{% endhighlight %}


#### Examples:

{% highlight powershell %}
alias testing 'echo "1, 2, $args!"' && . $PROFILE
# > testing 5
# Output: 1, 2, 5!

alias gc-m 'git commit -m "$args"' && . $PROFILE
# > gc-m "init"
# Equal to: git commit -m "init"
{% endhighlight %}
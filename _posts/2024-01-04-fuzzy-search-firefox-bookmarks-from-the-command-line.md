---
layout: post
title: Fuzzy Search Firefox Bookmarks from the Command-Line
date: 2024-01-04 22:13 -0800
description: Development related tips and tricks from an experienced developer.
categories:
- cli
- powershell
---

Tools you'll need:
* [Powershell v7+](https://www.microsoft.com/store/apps/9MZ1SNWT0N5D){:target="_blank"}
* [Sqlite](https://www.sqlite.org/index.html){:target="_blank"}
* [FZF](https://github.com/junegunn/fzf){:target="_blank"}
* Cut & Xargs: [How to use in Powershell](/cli/powershell/2024/01/13/using-gnu-utilities-in-powershell.html)

I'll demonstrate adding a Powershell alias below, but due to using cross-platform tools, the final command used should be fairly similar when used in a Bash / ZSH alias.

Open your Powershell profile in your editor:

{% highlight powershell %}
code $PROFILE
# Or use micro / vim / notepad / etc.
{% endhighlight %}
<br />
Next, add the following function and alias:

{% highlight powershell %}
# Replace <YOUR PROFILE> with your own path.
# Go to %APPDATA%\Mozilla\Firefox\Profiles\ look for ".default" in the name
# Update the Firefox.exe path at the end if needed.

function _ffb {sqlite3 C:\Users\AppData\Roaming\Mozilla\Firefox\Profiles\<YOUR PROFILE>\places.sqlite "select mbp.title,REPLACE(mb.title,'|','::'),mp.url from moz_bookmarks mb LEFT JOIN moz_bookmarks mbp ON mb.parent = mbp.id LEFT JOIN moz_places mp ON mb.fk = mp.id WHERE mb.type = 1;" | fzf | cut -d'|' -f3 | xargs "C:\Program Files\Mozilla Firefox\firefox.exe" {}}
Set-Alias -Name ffb -Value _ffb
{% endhighlight %}

Run ```. $PROFILE``` (*remember the dot*) to reload your profile.

Now simply type `ffb` (for "**F**ire**F**ox **B**ookmarks) to do a fuzzy search on your bookmarks by folder, title, and url from the command-line, and have it open in FF.

#### Examples

![Example Search](/assets/img/firefox-bookmarks-search-ex1.png)

![Example Search](/assets/img/firefox-bookmarks-search-ex2.png)

![Example Search](/assets/img/firefox-bookmarks-search-ex3.png)

Note: Any bookmarks with a `|` in their name will use `::` in the search to avoid conflicting with the SQL output format.  This will not edit your bookmarks.

*More info: [Profiles - Where Firefox stores your bookmarks, passwords and other user data](https://support.mozilla.org/en-US/kb/profiles-where-firefox-stores-user-data){:target="_blank"}*
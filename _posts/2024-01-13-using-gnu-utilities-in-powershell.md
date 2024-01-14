---
layout: post
title: Using GNU Utilities in Powershell
date: 2024-01-13 17:08 -0800
description: Development related tips and tricks from an experienced developer.
categories:
- cli
- powershell
---

It is possible to use various staple Linux commands such as `cut`, `grep`, `ls`, `find`, and even `xargs` in Powershell on Windows, without using WSL or Cygwin's environment.

#### Example Setup

* Install [Cygwin](https://cygwin.com/){:target="_blank"}
* Use in Powershell by adding (e.g.) `C:\cygwin64\bin` to your ***end*** of your PATH.
* Restart Powershell

We install [Cygwin](https://cygwin.com/){:target="_blank"}, but only for some of the utilities it comes with.  Please note: Powershell will not know how to handle the non-exe utilities in the folder if you call them, and you may run into conflicts with some in the folder such as `python` depending on the order of your PATH items.

Be sure to place the `cygwin64/bin` folder at the ***end*** of your path, and make sure any future installations of Python come ahead of Cygwin, in order to avoid issues.

For any name conflicts where you wish to use the new utility, such as `find`, simply [set an alias](/cli/powershell/2023/12/31/create-a-permanent-powershell-alias-from-the-command-line.html) with the full path of `C:\cygwin64\bin\find.exe`.

#### Usage

Get a list of the size and date of the files in the current directory:

```ls -lh | cut -d' ' -f8-```

<br/>

Get a list of the .EXE files in `C:\cygwin64\bin`:

```ls C:\cygwin64\bin | grep -o '.*.exe'```

#### Alternatives

There are a few other ways to go about this as well.  For example, [Git Bash](https://gitforwindows.org/){:target="_blank"} comes with several native tools, and [MSYS2](https://www.msys2.org/){:target="_blank"} makes it easy to find or compile new native Windows tools in many cases.

If you're just looking to use some of the more common utilities available on Linux in Powershell however, [Cygwin](https://cygwin.com/){:target="_blank"} offers a pretty good start.


*More info: [How to Edit Environment Variables on Windows 10 or 11 - How-To Geek](https://www.howtogeek.com/787217/how-to-edit-environment-variables-on-windows-10-or-11/){:target="_blank"}*
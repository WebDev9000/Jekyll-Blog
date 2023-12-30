---
layout: post
title: Input Text into a Command-Line Argument from an Editor
date: 2023-12-18 09:17 -0800
description: Development related tips and tricks from an experienced developer.
categories:
---

The convienient open source editor [Micro](https://github.com/zyedidia/micro) has a nice feature which allows it to easily create buffers from stdin, and send the data of the open buffer to the pipe when it exits.

For example: ```ifconfig | micro | cat```

Similarly, you can use Micro in a subprocess to "inject" text into a CLI command.
E.g. with [Llama.cpp](https://github.com/ggerganov/llama.cpp):

{% highlight powershell %}
./main -ngl 8 --color -c 2048 --temp 0.7 --repeat_penalty 1.1 -n -1 -p "$(micro)"
{% endhighlight %}

This will start the Micro editor, where you can enter (potentially large amounts of) formatted text for use as the LLM's prompt, without needing to save to a file or make a temporary file.

It works well in scripts:

{% highlight powershell %}
$prompt = $args[0]
# If no prompt, start an editor
if (!$prompt) {
  $prompt = "$(micro)"
}
invoke-expression "D:\llamacpp\main.exe -p '$prompt'"
{% endhighlight %}

and it also only stores "$(micro)" in your command history, which avoids long input clutter.

### Opening a file in the editor

While opening a file inside Micro after-the-fact doesn't appear to correctly pass the information back to the CLI, you *can* start with a file quite easily with:

{% highlight powershell %}
# CLI
./main -p "$(micro D:\myfile.txt)"
{% endhighlight %}

{% highlight powershell %}
# Script
$file = "D:/myfile.txt"
$prompt = "$(micro $file)"
invoke-expression "D:\llamacpp\main.exe -p '$prompt'"
{% endhighlight %}

This will start the editor with the file open, *and* pass any changes back to the command-line on exit ***without*** modifying the original file.
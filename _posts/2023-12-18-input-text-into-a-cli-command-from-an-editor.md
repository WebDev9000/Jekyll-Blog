---
layout: post
title: Input Text into a CLI Command from an Editor
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
# If no prompt, start an editor
if (!$prompt) {
  $prompt = "$(micro)";
}
{% endhighlight %}

and it also only stores "$(micro)" in your command history, which avoids long input clutter.

---
title: Transfer Stable Diffusion WebUI prompt metadata between two JPEG or PNG files
layout: post
description: Development related tips and tricks from an experienced developer.
date: '2023-10-31 14:36:12 -0700'
categories:
- tools
- ai-art
- cli
---

First, Download [ExifTool][exiftool]{:target="_blank"} from the official website.  Then:

{% highlight powershell %}
# Files must be the same extension
exiftool -TagsFromFile FileA.jpeg -overwrite_original FileB.jpeg
{% endhighlight %}
<br/>
For `.PNG` files, the following must be included in `.ExifTool_config` in the user's `HOME` directory:

{% highlight config %}
%Image::ExifTool::UserDefined = (
    'Image::ExifTool::PNG::TextualData' => {
        parameters => { }
    },
);
{% endhighlight %}

Note that transferring between a `.JPEG` and a `.PNG` file is not supported with this method.

*More info: [ExifTool FAQ][exiftool-faq]{:target="_blank"}*

[exiftool]: https://exiftool.org
[exiftool-faq]: https://exiftool.org/faq.html

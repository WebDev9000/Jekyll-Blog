---
layout: post
title: "Transfer Stable Diffusion WebUI prompt metadata between two JPEG or PNG files"
description: "Development related tips and tricks from an experienced developer."
date: 2023-10-31 14:36:12 -0700
categories: tools ai-art cli
---

Download [ExifTool][exiftool]

{% highlight powershell %}
# Files must be the same extension
exiftool -TagsFromFile FileA.jpeg -overwrite_original FileB.jpeg
{% endhighlight %}
<br />

For `.PNG` files, the following must be included in `.ExifTool_config` in the user's `HOME` directory.

{% highlight config %}
%Image::ExifTool::UserDefined = (
    'Image::ExifTool::PNG::TextualData' => {
        parameters => { }
    },
);
{% endhighlight %}
<br />

Note: transferring between a `.JPEG` and a `.PNG` file is not supported with this method.

*Source: [ExifTool FAQ][exiftool-faq]*

[exiftool]: https://exiftool.org
[exiftool-faq]: https://exiftool.org/faq.html
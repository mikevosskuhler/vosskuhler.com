---
layout: blog
title:  "Adding download link to blog page"
date:   2021-02-05 01:30:00 +0200
categories: jekyll update
---
# Add the file to a folder called downloads in the root directory
This website was build using the jekyll static site generator, the bootstrap framework, and the fontawesome icon library. In this post I will discuss the basic of these tools and how to quickly get started with building your own static websites. 

## Create a link to the file in your blog post
```
{% raw  %}
{{ site.url }}/downloads/<your file name>
{% endraw %}
```

## Working example
[download link]({{ site.url }}/downloads/hello.bin)
[download link]({{ site.url }}/downloads/cabfile.diagcab)
[download link]({{ site.url }}/downloads/cabfile.mini.diagcab)

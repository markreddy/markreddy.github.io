---

title: Elegantly uninstall all the gems
description: "How to rid your OSX system of all ruby gems in one line"
tags: [tutorial, ruby, bash, mac, hack]
comments: true
image:
  feature: texture-feature-01.jpg
---

There are instances where I would like to revert and uninstall all previous gem installations.<br><br>
For instance, when I first started using Ruby and didn't I use RVM....well that was a nightmare. So before migrating to RVM I needed a solution to elegantly uninstall all of the gems on my OSX system.<br><br>
Here is a nice one-liner that done what I needed:

{% highlight bash %}
for i in `gem list --no-versions`; do gem uninstall -aIx $i; done
{% endhighlight %}

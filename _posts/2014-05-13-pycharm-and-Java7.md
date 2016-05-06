---

title: PyCharm and Java7
description: "How to get PyCharm working with Java7"
tags: [tutorial, python, java, hack]
comments: true
image:
  feature: texture-feature-01.jpg
---

PyCharm is my python IDE of choice, however after updating my JDK from 6 to 7 I started getting the following:  
![PyCharm Warning Image]({{ site.url }}/images/pycharm-warning.png)  
Of course the answer was no and I just wanted it to work with Java7. Knowing a little bit about how apps are structured I went in search of PyCharm’s Info.plist (the information Property list is a structured text file that contains essential configuration information for a bundled executable). Within that file I could see where the restriction for Java6 came from, bingo.<br><br>
Steps:<br><br>
Use the Show Package Contents option in PyCharm bundle. Inside the Contents folder there is a Info.plist file, open it and find the following text:

{% highlight css %}<key>JVMVersion</key> <string>1.6*</string>{% endhighlight %}

Change it to:  

{% highlight css %}<key>JVMVersion</key> <string>1.7*</string>{% endhighlight %}

Save the Info.plist file and then run PyCharm as normal. You should not see the warning message now and PyCharm will run correctly.
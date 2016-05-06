---

title: Creating a new file in Finder using AppleScript
description: "Create a new file and open it in your editor of choice via finder"
tags: [tutorial, applescript, mac, macosx, finder, hack]
comments: true
image:
  feature: texture-feature-01.jpg
---

As much as I use the command line I often find myself navigating directories and making edits with Finder. Probably the only thing that annoyed me when doing so was it's inability to create a new text file. So after getting fed up with this I opened up my AppleScript Editor and in one line resolved my issue.

{% highlight applescript %}
tell application "Finder" to make new file with properties {name:"untitled.txt"} at (the target of the front window) as alias
{% endhighlight %}

I then exported this as an application dropped it into the Applications folder and cmd+dragged it onto the finder toolbar. I can now click it and a new untitled.txt file will appear in the directory I am in. Perfect.<br><br>
Taking it a little further, what is the most obvious thing I want to do after creating an empty text file, you guessed it, open the sucker! As [Atom](https://atom.io/) is my new editor of choice I added the following lines:

{% highlight applescript %}
tell application "Atom"
	open "untitled.txt"
end tell
{% endhighlight %}

Boom, a new file created and opened in my favourite text editor without the need to install any apps that do more than I need. I'm happy.


Full script:
{% highlight applescript %}
tell application "Finder" to make new file with properties {name:"untitled.txt"} at (the target of the front window) as alias
tell application "Atom"
	open "untitled.txt"
end tell
{% endhighlight %}

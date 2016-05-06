---

title: Comments in JSON
description: "How can you add comments to a JSON file"
tags: [tutorial, json, comments, hack]
comments: true
image:
  feature: texture-feature-01.jpg
---

Recently I was asked if you could write comments in JSON, just like you can in any common programming language. I was stumped for a second, I’ve never seen them, never wanted to comment my JSON so I needed to do some quick investigation to see if it was possible. Well it is, however there is no support or standard for comments in JSON. Here is a post from the Douglas Crockford one of JSON’s most prominent figures on the issue.

> I removed comments from JSON because I saw people were using them to hold parsing directives, a practice which would have destroyed interoperability. I know that the lack of comments makes some people sad, but it shouldn't. <br><br>
> Suppose you are using JSON to keep configuration files, which you would like to annotate. Go ahead and insert all the comments you like. Then pipe it through JSMin before handing it to your JSON parser.﻿

Here are a few ways of adding comments to your JSON:<br><br>
**C style comments:**  
As Crockford stated, you can add comments all you want, referring to C stye comments:

	single line // and multiline /*…*/

However this will not result in well formed JSON, you will need to “pipe it through JSMin before handing it to your JSON parser”. Sending it through JSMin will remove any C style comments from the JSON.<br><br>
**Designated comment element:**  
You could have a designated data element called “_comment” that would hold comments:

	“_comment” : “comment text goes here…”,

This of course would then need to be ignored by apps that retrieve this JSON data.<br><br>
**Use YAML:**  
Consider using YAML. It’s nearly a superset of JSON (virtually all valid JSON is valid YAML) and it allows comments. An example of comments in YAML:  

	# Set a custom port to listen for HTTP traffic:  
	http.port: 9200

<br>
After digging in and finding several ways to approach comments in JSON I’m going to stick with my original opinion, don’t do it.
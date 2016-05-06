---

title: Unix Command - man
description: "Use of the man command to help you "
tags: [tutorial, man, unix, help, manual]
comments: true
image:
  feature: texture-feature-01.jpg
---

Recently I have been working more and more frequently in a *nix environment (thats not to say I haven’t spent my fair share of time in the terminal). While running a few commands that I ‘just know’ how to run, I dug into them a bit deeper to find out their true functionality and get more acquainted with them. As I was doing this I thought “This would make for an interesting category for my blog – Unix Commands Expanded”. However, then I thought anything I write up, the ‘man’ command would do a better job than I ever could. So this article will introduce you to the ‘man’ command and from there navigating a *nix terminal should be a breeze.<br><br>
To use the man command, at the Unix prompt, enter:

	man topic
	

Replace topic with the name of the manual item about which you want more information. For example, to find out more about the FTP command, at the Unix prompt, enter:


	man ftp
	

If you are unsure which manual item you want to read, you can do a keyword search. At the Unix prompt, enter:


	man -k keyword | more
	

On some systems, you need to replace man -k with apropos. For example, at the Unix prompt, enter:


	apropos keyword | more
	

In both of the examples above, replace keyword with a specific topic (e.g., ftp, mail).<br><br>
For more information about the man command, at the Unix prompt, enter:


	man man

---

title: Installing Homebrew on Mac OSX
description: "How to install home-brew on Mac OSX"
tags: [tutorial, homebrew, mac, osx, package, install]
comments: true
image:
  feature: texture-feature-01.jpg
---

Homebrew is a package management system written by Max Howell that simplifies the installation of software on the Mac OS X operating system. It is a free/open source software project to simplify installation of other free/open source software packages. It is similar in aim and function to MacPorts and Fink.<br><br>
The installation is very straightforward, simply run the following command from your terminal:

	ruby -e "$(curl -fsSL https://raw.github.com/mxcl/homebrew/go)"

This will install brew, then run:

	brew doctor
	

Brew doctor will diagnose any known issues and sometimes give details on how to fix it. If not, you’re probably not the only one, google is your friend.<br><br>
Now we want to update Homebrew to make sure we’re getting the latest formulas:

	brew update 
	

And now we can test it out by running a simple command to instal wget on our machines:

	brew install wget
	


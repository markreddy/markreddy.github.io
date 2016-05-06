---

title: JUnit Assert
description: "Which One to Choose?"
tags: [tutorial, java, junit, testing, assert]
comments: true
image:
  feature: texture-feature-01.jpg
---

Unit tests, the bane of any engineers day, but a necessity and something that has proven itself to me over time to be invaluable if done correctly.<br><br>
For any developer that has just sat down to write their first test they may be confronted with the following problem when trying to use JUnit’s Assert functionality.<br><br>
JUnit framework contains 2 Assert classes:

* junit.framework.Assert
* org.junit.Assert


Why is this and which one do I choose?<br><br>
Well the old method of  writing JUnit3 classes was to extend junit.framework.TestCase. That inherited *junit.framework.Assert* and your test class gained the ability to call the assert methods.<br><br>
Since JUnit4 the framework was refactored in several areas and now uses the package name org.junit, which follows the standard conventions for package naming. It also takes advantage of Annotations for marking tests (@Test) amongst other things, which means you  no longer need to extend TestCase. But at the same time that also means that the assert methods are not inherently available for use.<br><br>
You now need to make a static import of the new Assert class (looking into the Assert class you will notice all the assert methods are  static methods). So you can import it this way:

	import static org.junit.Assert;
	
After this static import, you can use this methods without prefix.
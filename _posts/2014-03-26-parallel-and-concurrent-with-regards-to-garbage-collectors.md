---

title: Parallel And Concurrent With Regard To Garbage Collection
description: "What do the terms Parallel and Concurrent mean when describing Garbage Collection"
tags: [java, jvm, gc, parallel, concurrent ]
comments: true
image:
  feature: texture-feature-01.jpg
---

Although the words “Parallel” and “Concurrent” are used synonymously, when used in reference to Java garbage collection they are not the same. Unfortunately is can often lead to confusion when developers delve into the the world of the JVM and garbage collection, so lets clear it up here. <br><br>
Parallel collector belongs to the family of pure-stop-the-world collectors. That means, GC won’t kick in until JVM runs out of memory in the old-generation part of the heap. And when it starts all the mutator (application) threads will stop running. The reason it is called a Parallel collector is not because it runs in parallel to your application, it is because uses multiple GC threads for the GC operation.<br><br>
Where-as the concurrent collector (CMS) runs mostly-concurrent along with the other mutator (application) threads, and tries to free up memory so the mutator threads can keep on running. The reason is say most-concurrent is because it also stops-the-world for 2 very short time periods called initial-mark and remark phases.<br><br>
Hopefully that has cleared up some possibly tricky terminology when it comes to Java’s garbage collectors.
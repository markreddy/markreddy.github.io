---

title: Building Apache Spark with Scala 2.10
description: "How to gracefully and forcefully restart Jenkins"
tags: [tutorial, spark, scala, hack, apache]
comments: true
image:
  feature: texture-feature-01.jpg
---

[Apache Spark](http://spark.incubator.apache.org) is an open source cluster computing system that aims to make data analytics fast — both fast to run and fast to write.<br><br>
The latest release is [Spark 0.7.3](http://spark-project.org/download/spark-0.7.3-sources.tgz). But this release requires Scala 2.9.3. If you are using Scala 2.10, this release would not work.<br><br>
Since Spark has not announced any Scala 2.10 compatible release yet, so to build Spark with Scala 2.10, you have to download latest release from here: [Spark-Scala 2.10](https://github.com/mesos/spark/tree/scala-2.10).<br><br>
Installation instructions would be the same as previous release.<br><br>
Since Spark Api for this release is not available on any repository, so if you want to use it in your project, you need to do:<br><br>
Go to Spark directory<br><br>
Run sbt compile publish-local<br><br>
Add
````libraryDependencies += "org.spark-project" %% "spark-core" % "0.8.0-SNAPSHOT"````
in the build.sbt of your Scala project.
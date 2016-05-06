---

title: Unit Test Hanging During Sonar Analysis (JMockit, Maven, Sonar, JaCoCo and Jenkins)
description:
tags: [tutorial, java, jmockit, maven, sonar, jacoco, jenkins]
comments: true
image:
  feature: texture-feature-01.jpg
---

Recently I  deployed a new batch of unit tests based on the JMockit framework in our new Jenkins + Sonar environment and after building successfully the tests were hanging during sonar analysis. Even the tests that don’t use JMockit (simple JUnit) stopped to work. It was strange that during the build phase with test there was no problem but in the Sonar test phase the first JUnit test looped permanently.<br><br>
It took a while to figure out the problem, however I found that there is an incompatibility between JaCoCo and JMockit.<br><br>
To solve the issue I added the JMockit javaagent to the maven-surefire-plugin:

{% highlight xml %}
<argLine>
-javaagent:"${settings.localRepository}"
/com/googlecode/jmockit/jmockit/0.999.15/jmockit-0.999.15.jar
</argLine>
{% endhighlight %}


Here how it looks like the plugin:
{% highlight xml %}
<plugin>
 <groupId>org.apache.maven.plugins</groupId>
 <artifactId>maven-surefire-plugin</artifactId>
 <version>2.12</version>
 <configuration>
 <argLine>-javaagent:"${settings.localRepository}"/com/googlecode/jmockit/jmockit/0.999.15/jmockit-0.999.15.jar</argLine>
 </configuration>
 </plugin>
 {% endhighlight %}
 
After this change the test are executed correctly, the incompatibility between JaCoCo and JMockit had been solved and the analysis ran to completion show 98% unit test coverage!
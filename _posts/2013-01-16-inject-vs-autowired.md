---

title: Inject vs Autowired
description: "Spring, Inject vs Autowired"
tags: [tutorial, java, ioc, inject, auto wired, spring, framework]
comments: true
image:
  feature: texture-feature-01.jpg
---

The annotation @Inject (javax.inject.Inject) is part of the Java CDI standard introduced in Java EE 6 (JSR-330), which Spring has chosen to support using @Inject synonymously with their own @Autowired annotation.<br><br>
The annotation @Autowired is springs own annotation. @Inject is part of a new Java technology called CDI that defines a standard for dependency injection similar to Spring. In a spring application, the two annotations work in the same way as Spring has decided to support some JSR-330 annotations in addition to their own.<br><br>
Both of these annotations use the ‘AutowiredAnnotationBeanPostProcessor’ to inject dependencies.<br><br>
To add this functionality to you project, add the following to your pom.xml:
{% highlight xml %}
<dependency>
    <groupId>javax.inject</groupId>
    <artifactId>javax.inject</artifactId>
    <version>1</version>
</dependency>
{% endhighlight %}

Once the jar is on your classpath you can then leverage the functionality like so:

{% highlight java %}
package ie.mreddy.entity.dao;
 
import javax.inject.Named;
 
@Named
public class EntityDAO {
 
    public void save() {
        // impl
    }
}
{% endhighlight %}
 
{% highlight java %}
package ie.mreddy.entity.services;
 
import javax.inject.Inject;
import javax.inject.Named;
 
import ie.mreddy.entity.dao.EntityDAO;
 
@Named
public class EntityService {
    @Inject
    EntityDAO entityDAO;
 
    public void save() {
        System.out.println("Calling injected entityDAO's save method");
        entityDAO.save();
    }
}
{% endhighlight %}

There are some limitations on JSR-330 if you compare it to Spring’s counterpart:

* @Inject has no “required” attribute to make sure the bean is injected successful.
* In Spring container, JSR-330 has scope singleton by default, but you can use Spring’s @Scope to define others.
* No equivalent to Spring’s @Value, @Required or @Lazy.
---

title: Spring Autowiring using Qualifier Keyword
description:
tags: [tutorial, java, spring, framework, qualifier]
comments: true
image:
  feature: texture-feature-01.jpg
---

In Spring, the annotation @Qualifier specifies which bean is autowired on a field. The following scenario shows an instance where using @Autowired alone is not sufficent.<br><br>
**Autowiring Example**  
See below example, it will autowired a “person” bean into customer’s person property.

{% highlight java %}
package ie.markreddy;
 
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Qualifier;
 
public class Customer {
 
    @Autowired
    private Person person;
    //...
}
{% endhighlight %}

But, two similar beans “ie.markreddy.Person” are declared in bean configuration file. Will Spring know which person bean should autowired?

{% highlight xml %}
<beans xmlns="http://www.springframework.org/schema/beans"
 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
 xsi:schemaLocation="http://www.springframework.org/schema/beans
 
http://www.springframework.org/schema/beans/spring-beans-2.5.xsd">
 
<bean
class ="org.springframework.beans.factory.annotation.AutowiredAnnotationBeanPostProcessor"/>
 
 <bean id="customer" class="com.mkyong.common.Customer" />
 
 <bean id="personA" class="ie.markreddy.Person" >
 <property name="name" value="markA" />
 </bean>
 
 <bean id="personB" class="ie.markreddy.Person" >
 <property name="name" value="markB" />
 </bean>
 
</beans>
{% endhighlight %}

When you run above example, it hits below exception:

{% highlight java %}
Caused by: org.springframework.beans.factory.NoSuchBeanDefinitionException:
    No unique bean of type [ie.markreddy.Person] is defined:
        expected single matching bean but found 2: [personA, personB]
{% endhighlight %}


**@Qualifier Example**  
To fix above problem, you need @Qualifier to tell Spring about which bean should autowired.

{% highlight java %}
package ie.markreddy;
 
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Qualifier;
 
public class Customer {
 
    @Autowired
    @Qualifier("personA")
    private Person person;
    //...
}
{% endhighlight %}

In this case, bean “personA” is autowired.

	Customer [person=Person [name=markA]]

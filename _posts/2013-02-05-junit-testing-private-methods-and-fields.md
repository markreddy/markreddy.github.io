---

title: JUnit - Testing Private Methods and Fields
description: "How to gain access to private methods and fields for testing legacy code...."
tags: [tutorial, java, junit, reflection, hack]
comments: true
image:
  feature: texture-feature-01.jpg
---

I’m working with somewhat legacy code at the moment which needs to be tested. Unfortunately with most legacy code, changing it is something that is not within my current scope...even though the visibility of some fields need to be changed or getter/setters put in place to allow for testing. Also the addition of any new dependancies, such as PowerMock would be a long and drawn out approval process so that is out of the question. Alas, there is code that needs refactored and tests that must be completed beforehand to ensure the system isn't broken along the way.<br><br>
Found yourself in this situation? There is a solution, albeit not high on the 'sound software engineering' list which is...reflection! The best way I have found to test private methods/fields when you're so constrained is through the use of reflection.<br><br>
Internally we’re using helpers to get/set private and private static variables as well as invoke private and private static methods. The following patterns will let you do pretty much anything related to the private methods and fields. Of course you can’t change private static final variables through reflection.

{% highlight java %}
Method method = targetClass.getDeclaredMethod(methodName, argClasses);
method.setAccessible(true);
return method.invoke(targetObject, argObjects);
{% endhighlight %}

And for fields:
{% highlight java %}
Field field = targetClass.getDeclaredField(fieldName);
field.setAccessible(true);
field.set(object, value);
{% endhighlight %}

* targetClass.getDeclaredMethod(methodName, argClasses) lets you look into private methods. The same thing applies for getDeclaredField.
* The setAccessible(true) is required to play around with privates.

Of course once the refactor is complete the code will be much more robust and testable, removing any need for reflection.

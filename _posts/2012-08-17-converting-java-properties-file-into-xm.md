---

title: Converting Java Properties File into XML
description:
tags: [tutorial, java, xml, properties]
comments: true
image:
  feature: texture-feature-01.jpg
---

Many developers may not aware that the java.util.Properties class comes with a storeToXML() method to convert existing properties data into a XML file.

{% highlight java %}
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.OutputStream;
import java.util.Properties;
 
public class PropertiesXMLExample
{
    public static void main(String[] args) throws IOException
    {
        Properties props = new Properties();
        props.setProperty("email.support", "spamfilter@nospam.com");
 
        //where to store?
        OutputStream os = new FileOutputStream("c:/email-configuration.xml");
 
        //store the properties detail into a pre-defined XML file
        props.storeToXML(os, "Support Email","UTF-8");
 
        System.out.println("Done");
    }
}
{% endhighlight %}

The above example will write the properties detail into a XML file “c:/email-configuration.xml“.

{% highlight java %}
<?xml version="1.0" encoding="UTF-8" standalone="no"?>
<!DOCTYPE properties SYSTEM "http://java.sun.com/dtd/properties.dtd">
    <properties>
        <comment>Support Email</comment>
        <entry key="email.support">donot-spam-me@nospam.com</entry>
    </properties>
{% endhighlight %}

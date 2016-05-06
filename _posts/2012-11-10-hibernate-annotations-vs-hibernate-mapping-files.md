---

title: Hibernate Annotations vs. Hibernate Mapping Files
description:
tags: [tutorial, hibernate, annotations, mappings]
comments: true
image:
  feature: texture-feature-01.jpg
---

JPA annotations greatly simplify persistence programming with Hibernate, but to understand why they’re so great, it helps to understand what we needed to do before the introduction of annotations.<br><br>
Back to the Future: This Historical hibernate-mapping.xml File<br><br>
Hibernate makes persisting the state of your Java objects incredibly simple. However, in order for Hibernate to know where to story your JavaBeans, or how to map the property of a JavaBean to a database column, the developer has to provide a bit of direction to the Hibernate framework. As such, people developing Hibernate based applications had to maintain an unwieldily, monolithic mapping file that described how to save a given Java object to the database.<br><br>
So, for example, if you had a class named Event that had three properties, one called id, one called birthday, and another property called title, you would have to add the following segment to a hibernate-mapping file:

{% highlight xml %}
<hibernate-mapping>
    <class name="events.Event" table="EVENTS">
        <id name="id" column="id">
            <generator/>
        </id>
        <property name="birthday" type="timestamp"/>
        <property name="title"/>
    </class>
</hibernate-mapping>
{% endhighlight %}

What’s wrong with an XML mapping file?<br><br>
There is nothing inherently wrong, with a mapping file, and in fact, thousands of very salacious hibernate applications that are in production use an XML mappings file, but having a big XML mapping file presents a variety of non-lethal, but certainly annoying problems, including the following:

* Information about the Java class must be maintained in an external file
* XML isn’t always easy to write
* With lots of classes, the XML file can become unwieldily and massive
* Errors in one part of the XML file can ricochet all over your Java program

Anyway, Java 5 introduced a new Java based artefact – that annotation. Basically, an annotation allows you to add detail an information about a Java class, without damaging, disturbing or changing any of the code that is actually found inside a Java class or a Java method. So, instead of using a monolithic mappings file, Hibernate with JPA annotations allows you to completely rid applications of a mapping file, and instead, you can annotate your Java classes like so:

{% highlight java %}
@Entity
public class Event {
 
    private Long id;
    private String title;
    private Date date;
 
    @Id
    @GeneratedValue
    public Long getId(){
        return id;
    }
    private void setId(Long id){
        this.id = id;
    }
    public Date getDate() {
        return date;
    }
    public void setDate(Date date) {
        this.date = date;
    }
    public String getTitle() {
        return title;
    }
    public void setTitle(String title) {
        this.title = title;
    }
}
{% endhighlight %}

The @Entity, @Id and @GeneratedValue tags you see in the Event class are the JPA annotations, and they replace the neeed to describe how to persist your Java classes in an external hibernate-mappings.xml file. Instead of using an external file, each Java class maintains its own mapping information, which is much more natural, and much easier to maintain on a class by class basis. Furthermore, it makes introducing new classes, or even removing persistent classes from your domain model, much much easier.<br><br>
If you’re using Hibernate, and you have the ability to choose between using annotations or using a hibernate-mapping file, well, it’s really not much of a choice. Always use JPA annotations if you have a choice. JPA annotations are much easier to use, easy to maintain, and will help to make your Hibernate development experience a real pleasure. 
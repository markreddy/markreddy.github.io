---

title: Java7 Has Been Released
description:
tags: [java, release, jvm]
comments: true
image:
  feature: texture-feature-01.jpg
---

Oracle have just announced that Java 7 has been released!<br><br>
With years of hard work from their dedicated engineers, the largest team ever to work on the Java language and platform, as well as valuable input from the Java community, they have moved Java forward with this release.<br><br>
This release contains new language features (JSR 334), support for dynamic languages (JSR 292), a new multicore-ready API (JSR 166), new I/O APIs (JSR 203), and many other new features.<br><br>
Some of the features I’m most looking forward to are:<br><br>
**Strings in switch Statements**  
Did you know previous to Java 7 you could only do a switch on char, byte, short, int,Character, Byte, Short, Integer, or an enum type (spec)? Java 7 adds Strings making the switch instruction much friendlier to String inputs. The alternative before was to do with with if/else if/else statements paired with a bunch of String.equals() calls. The result is much cleaner and compact code.<br><br>
**Type Inference for Generic Instance Creation**  
Previously when using generics you had to specify the type twice, in the declaration and the constructor.  Java 7, you just use the diamond operator without the type.<br><br>
**Multiple Exception Handling Syntax**  
Tired of repetitive error handling code in “exception happy” APIs like java.io and java.lang.reflect?

{% highlight java %}
try {
    Class a = Class.forName("wrongClassName");
    Object instance = a.newInstance();
} catch (ClassNotFoundException ex) {
    System.out.println("Failed to create instance");
} catch (IllegalAccessException ex) {
    System.out.println("Failed to create instance");
} catch (InstantiationException ex) {
   System.out.println("Failed to create instance");
}
{% endhighlight %}

When the exception handling is basically the same, the improved catch operator now supports multiple exceptions in a single statement separated by "&#124;" (pipe).

{% highlight java %}
try {
    Class a = Class.forName("wrongClassName");
    Object instance = a.newInstance();
} catch (ClassNotFoundException | IllegalAccessException |
   InstantiationException ex) {
   System.out.println("Failed to create instance");
}
{% endhighlight %}

Sometimes developers use a “catch (Exception ex) to achieve a similar result, but that’s a dangerous idea because it makes code catch exceptions it can’t handle and instead should bubble up (IllegalArgumentException, OutOfMemoryError, etc.).<br><br>
**The try-with-resources Statement**  
The new try statement allows opening up a “resource” in a try block and automatically closing the resource when the block is done.<br><br>
For example, in this piece of code we open a file and print line by line to stdout, but pay close attention to the finally block;

{% highlight java %}
try {
    in = new BufferedReader(new FileReader("test.txt"));
 
    String line = null;
    while ((line = in.readLine()) != null) {
            System.out.println(line);
    }
} catch (IOException ex) {
    ex.printStackTrace();
} finally {
    try {
        if (in != null) in.close();
    } catch (IOException ex) {
        ex.printStackTrace();
    }
}
{% endhighlight %}

When using a resource that has to be closed, a finally block is needed to make sure the clean up code is executed even if there are exceptions thrown back (in this example we catch IOException but if we didn’t, finally would still be executed). The new try-with-resources statement allows us to automatically close these resources in a more compact set of code:

{% highlight java %}
try (BufferedReader in=new BufferedReader(new FileReader("test.txt")))
{
    String line = null;
    while ((line = in.readLine()) != null) {
    System.out.println(line);
}
} catch (IOException ex) {
    ex.printStackTrace();
}
{% endhighlight %}

So “in” will be closed automatically at the end of the try block because it implements an interface called java.lang.AutoCloseable. An additional benefit is we don’t have to call the awkward IOException on close(), and what this statement does is “suppress” the exception for us (although there is a mechanism to get that exception if needed, Throwable.getSuppressed()).<br><br>
**Improved File IO API**  
There are quite a bit of changes in the java.nio package. Many are geared towards performance improvements, but long awaited enhancements over java.io (specially java.io.File) have finally materialized in a new package called java.nio.file.<br><br>
For example, to read a small file and print all the lines (see example above):

{% highlight java %}
List<String> lines =  Files.readAllLines(
FileSystems.getDefault().getPath("test.txt"), StandardCharsets.UTF_8);
 
for (String line : lines) System.out.println(line);
{% endhighlight %}

java.nio.file.Path is an interface that pretty much serves as a replacement forjava.io.File, we need a java.nio.file.FileSystem to get paths, which you can get by using the java.nio.file.FileSystems factory (getDefault() gives you the default file system).<br><br>
java.nio.file.Files then provides static methods for file related operations. In this example we can read a whole file much more easily by using readAllLines(). This class also has methods to create symbolic links, which was impossible to do pre-Java 7. Another feature long overdue is the ability to set file permissions for POSIX compliant file systems via the Files.setPosixFilePermissions method. These are all long over due file related operations, impossible without JNI methods or System.exec() hacks.<br><br>
I didn’t have time to play with it but this package also contains a very interesting capability via the WatchService API which allows notification of file changes. You can for example, register directories you want to watch and get notified when a file is added, removed or updated. Before, this required manually polling the directories, which is not fun code to write.
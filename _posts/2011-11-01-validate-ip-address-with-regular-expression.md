---

title: Validate IP address with regular expression
description: "Java code to validate ups with regex"
tags: [tutorial, java]
comments: true
image:
  feature: texture-feature-01.jpg
---

**Regular Expression:**

	^([01]?\\d\\d?|2[0-4]\\d|25[0-5])\\.([01]?\\d\\d?|2[0-4]\\d|25[0-5])\\.
	([01]?\\d\\d?|2[0-4]\\d|25[0-5])\\.([01]?\\d\\d?|2[0-4]\\d|25[0-5])$

**Java Example:**

{% highlight java %}
package ie.markreddy.regex;
 
import java.util.regex.Matcher;
import java.util.regex.Pattern;
 
public class IPAddressValidator{
 
    private Pattern pattern;
    private Matcher matcher;
 
    private static final String IPADDRESS_PATTERN =
        "^([01]?\\d\\d?|2[0-4]\\d|25[0-5])\\." +
        "([01]?\\d\\d?|2[0-4]\\d|25[0-5])\\." +
        "([01]?\\d\\d?|2[0-4]\\d|25[0-5])\\." +
        "([01]?\\d\\d?|2[0-4]\\d|25[0-5])$";
 
    public IPAddressValidator(){
      pattern = Pattern.compile(IPADDRESS_PATTERN);
    }
 
   /**
    * Validate ip address with regular expression
    * @param ip ip address for validation
    * @return true valid ip address, false invalid ip address
    */
    public boolean validate(final String ip){
      matcher = pattern.matcher(ip);
      return matcher.matches();
    }
}
{% endhighlight %}

IP address that matches:  
1. “1.1.1.1″, “255.255.255.255″,”192.168.1.1″ ,  
2. “10.10.1.1″, “132.254.111.10″, “26.10.2.10″,  
3. “127.0.0.1″  
<br>
IP address that doesn’t match:  
1. “10.10.10″ – must have 4 “.”  
2. “10.10″ – must have 4 “.”  
3. “10″ – must have 4 “.”  
4. “a.a.a.a” – only digit has allowed  
5. “10.0.0.a” – only digit has allowed  
6. “10.10.10.256″ – digit must between [0-255]  
7. “222.222.2.999″ – digit must between [0-255]  
8. “999.10.10.20″ – digit must between [0-255]  
9. “2222.22.22.22″ – digit must between [0-255]  
10. “22.2222.22.2″ – digit must between [0-255]  
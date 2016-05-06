---

title: Getting Mac Address In Java
description: "How to get the localhost MAC address in Java"
tags: [tutorial, java, code]
comments: true
image:
  feature: texture-feature-01.jpg
---

Since JDK 1.6, Java developers are able to access network card detail via NetworkInterface class. In this example, I'll show you how to get the localhost MAC address in Java.<br><br>

{% highlight java %}
package ie.markreddy;
 
import java.net.InetAddress;
import java.net.NetworkInterface;
import java.net.SocketException;
import java.net.UnknownHostException;
 
public class NetworkApp{
 
   public static void main(String[] args){
 
    InetAddress ip;
    try {
 
        ip = InetAddress.getLocalHost();
        System.out.println("Current IP address : " + ip.getHostAddress());
 
        NetworkInterface network = NetworkInterface.getByInetAddress(ip);
 
        byte[] mac = network.getHardwareAddress();
 
        System.out.print("Current MAC address : ");
 
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < mac.length; i++) {
            sb.append(String.format("%02X%s", mac[i], (i < mac.length - 1) ? "-" : ""));
        }
        System.out.println(sb.toString());
 
    } catch (UnknownHostException e) {
 
        e.printStackTrace();
 
    } catch (SocketException e){
 
        e.printStackTrace();
 
    }
 
   }
 
}
{% endhighlight %}

**Note**  
This NetworkInterfaceNetworkInterface.getHardwareAddress() method is only allowed to access localhost MAC address, not remote host MAC address.
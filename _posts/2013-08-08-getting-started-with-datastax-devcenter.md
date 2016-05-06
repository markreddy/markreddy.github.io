---

title: Getting started with DataStax DevCenter
description: "At quick intro into DataStax's DevCenter"
tags: [tutorial, cassandra, dse, datastax, nosql, devcenter]
comments: true
image:
  feature: texture-feature-01.jpg
---

DevCenter is a free, Eclipse-based tool from DataStax, for those of you who do not know who DataStax are, they contribute, distribute and offer commercial support for their enterprise edition of Apache Cassandra. DevCenter itself is designed to be a lightweight visual interface that provides developers with the ability to easily run CQL queries against Cassandra, view query results, and perform other related tasks.<br><br>
It looks like a ‘very’ light version of Oracle SQL Developer, that however is not a bad thing. If it can reach the feature set of SQLDeveloper it will be a fantastic addition to any Cassandra developers tool belt. As the app is still only in alpha so not much is expected, however what is expected is there, the ability to connect to a cluster, query it, open multiple query tabs and save those queries.<br><br>
To open a connection go to the connection panel and click the plug+ icon or right click anywhere in the panel and click open connection, this will bring up a Connections dialog, where you enter a name for the cluster (does not have to match the actual cluster name) and the IP to connect to:
![devcenter connection]({{ site.url }}/images/devcenter-connection.jpg)<br><br>
Click ‘Test Connection’ to verify the host is correct, this is where some of the UX of devCenter fails down a little, if it is successful you will see the following:
![devcenter success]({{ site.url }}/images/devcenter-success.jpg)<br><br>
This progress dialog will quickly disappear with no indication of success, so in this case ‘no news, is good news’. If there was a failure in validating the host, you would see:
![devcenter fail]({{ site.url }}/images/devcenter-fail.jpg)<br><br>
Once you have clicked ok, you will see your newly created connection in the Connections panel (top left). To connect to a cluster simply right click on the Connection Name and hit Open Connection.  
![devcenter open]({{ site.url }}/images/devcenter-open.jpg)<br><br>
Now we are connected we can start to querying our Cassandra cluster. Lets run through a quick example of creating a keyspace and a table, then inserting data, updating it and finally reading it.<br><br>
Keyspace creation:  
![devcenter keyspace]({{ site.url }}/images/devcenter-keyspace.jpg)<br><br>
Table creation:  
![devcenter create]({{ site.url }}/images/devcenter-create.jpg)<br><br>
Inserting some data:  
![devcenter insert]({{ site.url }}/images/devcenter-insert.jpg)<br><br>
Reading the data we just inserted:  
![devcenter select]({{ site.url }}/images/devcenter-select.jpg)<br><br>
Updating the data and reading the newly updated data:  
![devcenter update]({{ site.url }}/images/devcenter-update.jpg)<br><br>
Pressing the green play icon will execute these commands against your cluster.<br><br>
And that is it in a nutshell, connection, full support for CQL, tabs and saving your queries. A great platform to release into alpha and the roadmap looks good, with syntax highlighting and code assist coming in the next milestone. For more information visit the [DataStax blog](http://www.datastax.com/2013/08/introducing-datastax-devcenter).<br><br>
DevCenter can be downloaded from [here](http://www.datastax.com/download#dl-devcenter). If you have any feedback on the application drop the guys at DataStax a mail: devcenter-feedback@datastax.com<br><br>
Questions? Feel free to post in the comments section below.
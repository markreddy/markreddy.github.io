---
title: "Cassandra - List all tokens assigned to a virtual node"
categories:
  - Scripts
tags:
  - Cassandra
  - Scripts
---

After working with vnodes for some time now I would recommend that you always populate initial_token. If you run with the default 256 tokens it would be a tedious task to get the tokens of all the nodes in your cluster. So to aid in this process here are two nice scripts that will parse out those tokens for you.<br><br>
This one liner gets a list of only the tokens assigned to the node you are connected to:

{% highlight bash %}
nodetool info -T | grep Token | awk '{print $3}' | paste -s -d,
{% endhighlight %}

Which will output a string of all 256 tokens comma deliminated.<br><br>
If you want to get a list of tokens for all nodes in the cluster the following will do so:

{% highlight bash %}
for i in $(nodetool status | awk '/UN/{print $2}'); do
echo "#${i}"
printf "initial_token: ";
list=$(nodetool ring | awk '/'${i}'/{print $NF}'| paste -s -d)
echo ${list%,*}
done
{% endhighlight %}

Which will output each node's IP and the initial_token populated with the relevant tokens.

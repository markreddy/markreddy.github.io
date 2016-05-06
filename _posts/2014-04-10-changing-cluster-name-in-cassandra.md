---

title: Changing Cluster Name In Cassandra
description: "How to change the name of a cluster in Cassandra"
tags: [tutorial, python, java, hack]
comments: true
image:
  feature: texture-feature-01.jpg
---

As of Cassandra 1.2.x you can do the following:

1. Start the cqlsh connected locally to the node.
2. Run:  
````update system.local set cluster_name='$CLUSTER_NAME' where key='local';````  
3. Run nodetool flush on the node.
4. Update the cassandra.yaml file on the node, changing the cluster_name to the same as you set in step 2.
5. Restart the node.

Please be aware that you will have two partial clusters until you complete your rolling restart. Also considering that the cluster name is only a cosmetic value my opinion would be to leave it, as the risk far outweighs the benefits of changing it.
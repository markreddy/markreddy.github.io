---

title: Running two Elasticsearch instances on one machine
description: "How to run two Elasticsearch instances on one machine"
tags: [tutorial, elasticsearch, config, hack]
comments: true
image:
  feature: texture-feature-01.jpg
---

Elasticsearch by default runs assuming a one machine, one node setup. However for local dev I needed to boot up more than one node on my machine, to test certain aspects of a cluster and for my own personal exposure.<br><br>
The quickest way I though of was to specify parameters via the cli when starting a new instance, for example:

    $ bin/elasticsearch -Des.node.master=true -Des.node.name=Node1 ...
    $ bin/elasticsearch -Des.node.master=false -Des.node.name=Node2 ...
    $ bin/elasticsearch -Des.node.master=false -Des.node.name=Node3 ... 
    

However this can get tedious, passing in params for each node started, every time you want to start one.
So the most convient answer is to create multiple elasticsearch.yml files (elasticsearch.1.yml, elasticsearch.2.yml etc) and then start each instance from the command line referencing the new config files:

    $ bin/elasticsearch -Des.config=$ES_HOME/config/elasticsearch.1.yml
    $ bin/elasticsearch -Des.config=$ES_HOME/config/elasticsearch.2.yml
    $ bin/elasticsearch -Des.config=$ES_HOME/config/elasticsearch.testNoData.yml
    


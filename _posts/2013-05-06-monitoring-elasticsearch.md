---

title: Monitoring Elasticsearch
description: "How to monitor Elasticsearch using New Relic"
tags: [tutorial, new relic, elasticsearch, monitoring, ops, perf]
comments: true
image:
  feature: texture-feature-01.jpg
---

Two of my favourite applications at the moment are Elasticsearch and New Relic. Elasticsearch is a distributed, RESTful, free/open source search server based on Apache Lucene, while New Relic is a software as a service (SaaS) based application performance management (APM) tool that can monitor a wide range of applications, written various different languages. I have been using New Relic in a production environment for some time now, on the other hand I have only recently deployed ES into the same. As ES is the new kid on the block in the search space, there is no real standard/optimal configuration for different scenarios, it really is on each developer to benchmark their own use case and tinker with the config until they are satisfied. Concerned that my configuration of ES may have not been optimal for my use case, I went in search for some monitoring tools to help me evaluate the state of my cluster under production load and diagnose any problems as they arise.<br><br>
Initially I used the likes of Head, BigDesk and Paramedic during the proof of concept (POC) phase of development.  These tools are fantastic for real time analysis of an ES cluster, during testing I was able to hop on an monitor every aspect of my cluster. This was great, but I needed a tool that would store historical data spanning weeks/months, something like the functionality that New Relic provides, I bet you know where I am going with this….After digging around I found this [Elasticsearch-NewRelic Plugin](https://github.com/viniciusccarvalho/elasticsearch-newrelic).<br><br>
This plugin gathers all the metrics I need and sends them back to New Relic via New Relic’s java agent. Here is just a small sample for what it can report on:<br><br><br>
![ES NewRelic]({{ site.url }}/images/es-newrelic1.png)  
![ES NewRelic]({{ site.url }}/images/es-newrelic2.png)  
![ES NewRelic]({{ site.url }}/images/es-newrelic.png)  
<br><br>
To install New Relic’s java agent and the elasticsearch-newrelic plugin, please read this follow up post: [Ealsticsearch and New Relic]({{ site.url }}/elasticsearch-and-new-relic/).
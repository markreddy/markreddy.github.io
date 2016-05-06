---

title: Upgrading CpsCenter From 3.2 to 4.0 - Agent Trouble
description: "When upgrading DSE OpsCenter I ran into the following issue"
tags: [tutorial, jenkins]
comments: true
image:
  feature: texture-feature-01.jpg
---

I was running  DataStax OpsCenter version 3.2, once the 4.0 release was made available I began the install procedure. Eventything worked as expected until I attempted to install the new datastax-agents on the Cassandra nodes.<br><br>
The option to ‘Fix’ was available, however the install process failed. The resulting log indicated that there was a conflict between ‘ opscenter-agent’ and ‘datastax-agent’. I had assumed the install (Fix) process would handle that fact, but it did not.<br><br>
To get the datastax-agent installed correctly I had to:

1. I completely removed the opscenter-agent
2. Manually install the datastax-agent


To do this I ran the following on each node:  
````sudo service opscenter-agent stop````  
````sudo apt-get --purge remove opscenter-agent````  
````sudo apt-get install datastax-agent````  
````sudo service datastax-agent start````

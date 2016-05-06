---

title: Elasticsearch and New Relic
description: "How to Integrate Elasticsearch and New Relic"
tags: [tutorial, new relic, java, elasticsearch, integration]
comments: true
image:
  feature: texture-feature-01.jpg
---

The installation of the Elasticsearch-NewRelic plugin is quite straightforward.<br><br>
First we need to download and install New Relic’s Java Agent, this agent is responsible for sending back all the statistical data to New Relic’s servers, for storage, charting, etc.<br><br>
To obtain the latest Java Agent from New Relic we must:

* Log in to New Relic.
* Go to the Account Settings section.
* Download the Java agent from the list of ‘latest agents’.

Now that we have the agent, it is just a matter of installing it:

* In your app server’s root directory, create a new directory named newrelic.
* Unpack the downloaded file into the newrelic directory.


To have New Relic start up when Elasticsearch starts we can edit the elasticsearch.in.sh script located in the bin directory and add this line:<br><br>

````JAVA_OPTS="$JAVA_OPTS -javaagent:/$ES_HOME/newrelic/newrelic.jar"````<br><br>
Log into your NR account and within a few minutes you will see statistical data on the OS and JVM being populated for your ES instance. Now that we have New Relic running, we can install the Elasticsearch-NewRelic plugin to allow us to monitor ES itself. The plugin can be obtained from [here](https://github.com/viniciusccarvalho/elasticsearch-newrelic). We need to build the plugin using gradle. I work on a Mac (OSX), so I can run the following command to install gradle:<br><br>

````brew install gradle```` <br><br>
If you do not have brew installed, please check out my post on how to do so: Installing Homebrew on Mac OSX.<br><br>
To build the plugins Jar via gradle, navigate to the plugins root directory and run:<br><br>

````gradle jar````<br><br>
This will build a jar file called elasticsearch-newrelic-master-0.0.1.jar located in [build -> libs]<br><br>
To install the plugin, like all ES plugins we can run:<br><br>

````bin/plugin -url file://path/to/elasticsearch-newrelic-master-0.0.1.jar -install newrelic````<br><br>
That should be it for the setup, with the Java agent and plugin installed you can now monitor your ES instance with ease.<br><br>
Now to actually display the metrics collected by the plugin you will need to create a custom dashboard and from there you can create charts and tables. The plugin collects six main categories: indices, pool, network, transport, http and filesystem. The metrics are created using newrelic hierarchical approach, so for example:<br><br>
To  see the report on the total number of searches executed  you can type the following: indices/search/total or to group all metrics under an individual catagory you can do: indices/search/*
![Indexing Image]({{ site.url }}/images/indexing.png)<br><br>
For my own ease of use I like to create a custom dashboard for each individual catagory, as so:
![Dashboards Image]({{ site.url }}/images/dashboards.png)<br><br>
And that is it, you now have a historical data monitor for your Elasticsearch cluster.
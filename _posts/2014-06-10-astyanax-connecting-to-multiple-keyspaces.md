---

title: Astyanax - Connecting to multiple keyspaces
description: "How to connect to multiple keyspaces, using a single ConnectionPool"
tags: [tutorial, java, cassandra, astyanax]
comments: true
image:
  feature: texture-feature-01.jpg
---

When using cassandra, you often end up having more than one keyspace. In this scenario you have two options

* Create completely seperate cluster connections specifying the keyspace in each.
* Create a single cluster connection and reuse that for multiple keyspace connections.

Personally I find that for the majority of scenarios creating a single cluster connection is the preferred option and the cleanest.


{% highlight java %}
ConnectionPoolConfigurationImpl poolConfig = new ConnectionPoolConfigurationImpl("MyConnectionPool")
        .setPort(9160)
        .setMaxConnsPerHost(1)
        .setSeeds("127.0.0.1:9160")
        .setLatencyAwareUpdateInterval(10000)
        .setLatencyAwareResetInterval(0)
        .setLatencyAwareBadnessThreshold(2)
        .setLatencyAwareWindowSize(100);

AstyanaxContext.Builder builder = new AstyanaxContext.Builder();
AstyanaxContext<Cluster> clusterContext = builder
        .forCluster("Test Cluster")
        .withAstyanaxConfiguration(new AstyanaxConfigurationImpl()
                        .setDiscoveryType(NodeDiscoveryType.RING_DESCRIBE)
                        .setConnectionPoolType(ConnectionPoolType.TOKEN_AWARE)
        )
        .withConnectionPoolConfiguration(poolConfig)
        .withConnectionPoolMonitor(new CountingConnectionPoolMonitor())
        .buildCluster(ThriftFamilyFactory.getInstance());

clusterContext.start();
Cluster cluster = clusterContext.getClient();


Keyspace ks1 = cluster.getKeyspace("test1");
Keyspace ks2 = cluster.getKeyspace("test2");

// Test the connections by retrieving some data
System.out.println(ks1.describeKeyspace().getName());
System.out.println(ks2.describeKeyspace().getName());
{% endhighlight %}

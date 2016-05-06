---
title: Building scalable applications
description: "Lessons learned along the way to building some highly scalable application"
tags: [application, systems, architecture, software, java]
comments: true
image:
  feature: texture-feature-01.jpg
---

Building scalable applications is hard and over the past few years I've learned that the hard way. While these applications aren't at the scale of Facebook, Google or Twitter, they are of reasonable enough size where these lessons become valuable, once I progress to larger applications like those mentioned I'll be sure to share the strange and unusual problems that I'll encounter there too but for now here are some lessons I have learned so far:

## Instrumentation
Would you pilot a 747 plane with all the cockpit instruments blacked out, I sure wouldn't, so why do we often do the same with our code? We deploy it into production with no visible insight into what is happening with our applications.<br><br>
Getting the ball rolling and putting those initial few metrics in place can be very simple and yet very valuable. For example, requests per second and response time, simple. Request per seconds will tell us very clearly when we need to start adding capacity and response time will give performance feedback that may improve or deteriorate due to code changes.<br><br>
Instrumenting applications with metrics and performance stats gives everyone insight into what’s happening before the app comes plummeting back down.

## Code Defensively
Defend your application from those odd situations you can find yourself in. Take the two following examples:

- On start up it will attempt to establish connection to databases, queues, web services, etc. What happens when it can't connect to say the database. Will the application continue, start processing data and then error when it attempts to save to the DB?
- Your integrated with a 3rd party API, this integration is on the critical path of your code flow. The 3rd party API is down! Events on that code flow start to error, your application starts to gather a backlog, application performance starts to degrade.

These prime examples where you need to code defensively. Your application should gracefully handles these situations while at the same time raising the alarm so developers are made aware of the situation. You need to cover every area with some redundancy so you can offer the best possible experience.

## Automated Performance Testing
You have your unit tests, your code works.<br>
You have your integration test, your system as a whole works.<br><br>
What about those code changes that introduce regression in application performance? This is one set of test I rarely see companies put any effort into. Testing your code for increased response times is the only way to catch these types of regressions before they make it to production. Also don't just compare these results over a day or even a week, you will want compare over the past month at the very least. One of my personal favourite examples of how to do this correctly is Apache Lucene nightly benchmarks: http://people.apache.org/~mikemccand/lucenebench/

## Feature Flags
Having the ability to turn features or sub-sections of your application on/off at a moments notice is extremely valuable. These can be used in case of emergency for example, a new feature was deployed that contains a bug, with a feature flag you can very quickly turn it off preventing harm. If you invest more time you could also use it for A/B testing turning on a new feature for only 5% of your customers and monitoring progress.

## Dependancy awareness
This awareness needs to take place deep in the bowls of the application, yes I'm taking about library dependencies and the dependencies they drag in. If engineers are constantly evolving the product, new client libraries will be added and existing one will be updated. First of all ensure there is a process in place to accept new dependencies into your codebase and secondly ensure that those dependencies are visible across development teams so there are no clashes is vital to prevent those WTF moments when mixed versions interact. Those WTF moments when mixed versions interact can ruin a teams day and set a project back more than a few man hours.

## Cache
Cache that...oh cache that too, hey look we can cache this as well! Use memcache or redis to cache everything possible! Databases suck, don't connect to them unless you have to. Ensure that your caches are robust, you can invalidate them when the need arises and this procedure is repeatable, having an 'invalidation strategy' is key. The worst thing that could possibly happen is you invalidate your cache which results in a thundering heard effect on a cold DB...you may think that the query-cache in your database is efficient but it's not nearly efficient as you think. Cache all the things!

## Data Evolution Is Difficult And Expensive
Data evolution / manipulation at scale can be painstaking and if you are running multiple data stores it can be even worse. It is also a major drain on the resources of the system and possibly members of the development team.<br><br> Take for example changing a mapping in an Elasticsearch index, this will require a completed reindex of the mapping in question. What does this involve? Either reading the data from a secondary data store or reading it from Elasticsearch itself, either way this would require the development of long running job to iterate over all the necessary data ensuring that you sufficiently throttling reads/writes and not resurrecting deleted data, if you do deletes. Reading and writing a full data set will trash the cache, increase I/O, network and memory pressure. If you're using Cassandra or Mongo, changing a schema is simple but changing a BLOB structure or manipulating data over a huge data set will still lead to all the above negative impacts to the cluster.<br><br>
So how do you deal with this? Get you schema right the first time and never change it, simple. Not so simple, this would never work in a fast paced development environment, so all you can do is plan for the day it comes around, build you apps so they are loosely coupled with the data stores and extensible to schema changes, build buffers between data processing layers and your data stores so you can buffer writes when making changes. Ensure your developers know the pros and cons of reading a full data set such as memory limits, max read per second, network bandwidth so they can build the most efficient migration tools possible.<br><br><br><br>
After experiencing all of the above first hand, the first thing I generally said to myself was "Obviously, how didn't I know that before!" *facepalm*. But we all have to start somewhere and by me sharing this maybe you'll be better prepared when designing your next scalable application. If you have learned something along the way to building a highly scalable application please share your experiences in the comments.

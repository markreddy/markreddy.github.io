---

title: Elasticsearch Change In Routing Value Resulting In Duplicate Documents
description: "If you change the routing value of a doc and it goes to a different shard, duplicates will occur"
tags: [elasticsearch]
comments: true
image:
  feature: texture-feature-01.jpg
---

My current Elasticsearch project involves customers and orders. Customers and orders have a parent child relationship, with customer being the parent and order the child. The customer ID is used as the routing value, in some corner cases we are required to change the customer ID of an order.<br><br>
This is where it gets tricky. From an Elasticsearch point of view, a child is assigned to a particular shard based on the parent ID (customer ID). If you change the parent, then it tries to index that doc on a new shard (potentially, depending on which shard the new ID hashes to) but it doesn't know that it has to delete the old version on the old shard. There can be different documents with the same ID if they have different routing values. And child documents automatically get their parents' IDs as routing values. Thus leading to two customers having the same order associated with them.<br><br>
The only solution is to handle this scenario yourself.<br><br>
We are required on an update of an order to check if existing customer ID equals new customer ID. If this check returns false we issue a delete on the order, removing it completely from our index and then indexing the order with the new customer ID (routing value) this will ensure that no duplicates are created.<br><br>
I understand the intricacies of trying to handle this scenario within Elasticsearch itself and for that reason I don't think they will make any movement towards fixing this to give the end user the 'expected' behaviour.<br><br>
I hope this article was of use if you are currently facing this problem. There is an issue opened on Github here: [Issue #2663](https://github.com/elasticsearch/elasticsearch/issues/2663)
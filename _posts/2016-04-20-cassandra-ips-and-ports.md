---
layout: post
title:  ""
date:   2016-04-20 12:00:00 +0100
categories: 
---

## Title

clients using CQL: broadcast address + 9042
clients using Thrift: broadcast address + 9160

internode communication (replication, streaming): BROADCAST_ADDRESS (!)(?) + 7000
internode communication (replication, streaming) with enabled encryption: ??? + 7001

port OpsCenter opens to listen for Datastax Agents sending metrics: 61620
port Datastax Agent opens to listen for <???> sent from Opscenter: 61620


-- finish and turn into diagram with a nodes in two different dcs and opscenter and agents etc.

https://www.quora.com/Which-ports-does-Cassandra-use-and-how-are-they-used

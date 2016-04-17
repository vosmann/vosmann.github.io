---
layout: post
title:  "Migrating Cassandra"
date:   2016-04-17 15:00:00 +0100
categories: cassandra data storage
---

## What you can do:

- mix snitches
- mix versions (under the condition that your Cassandra clients specify the older Cassandra version's protocol version

E.g. like this in Java:

    ...
    .withProtocolVersion(ProtocolVersion.V2)
    ...




## What you can't do:

- add nodes running a old version after the clients already connected and started using an older ProtocolVersion.

Constraints: old version, gossiping snitch, ...



## Preparing EBS drives with Senza


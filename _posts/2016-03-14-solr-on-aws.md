---
layout: post
title:  "A reliable Zookeeperless Solr deployment on AWS"
date:   2016-03-14 21:00:00 +0100
categories: aws solr
---

## Intro

As stated on Solr's [home page](http://lucene.apache.org/solr/), Solr is a _popular, blazingly fast, open source
search platform built on Apache Lucene_. I've had the opportunity to work with Solr a lot these past few years and
to learn from the experiences of my seniors at Zalando. In this post I'd like to document some of my recent work
designing and implementing a fairly robust Solr deployment in a cloud environment.

The main problem being tackled here is one of resilience against unexpected machine failures, or in this case,
EC2 instance shutdowns. The hardware running your service will at some point either fail or require some kind of
maintenance that needs downtime. Being able to gracefully recover from the rug being pulled out from under your
service is a basic requirement for any service being run on a provider such as AWS.

The design proposed here works with all versions of Solr and removes the need for an external system like
Zookeeper for coordinating your cluster.

## Challenges
<!-- ## Points that need to be addressed -->

1. Bootstrapping a cluster
 - how to handle write path, how to handle read path. master/slave or?
 - filling the cluster with initial data.

2. Dealing with redeploys (e.g. schema changes)

3. Dealing with master failures
 - slaves will replicate empty

4. Dealing with slave failures
 - must get no reads

## Solr overview

### Vintage Solr (pre-5.0)

- Master-slave
- Force updates onto slaves or have slaves poll the master

### Modern Solr (5.0 and later)

- sharding (?)
- machines going down, promoting slaves to masters

## A reliable Zookeeperless Solr deployment on AWS

In my solution an older version of Solr was 

### The triple ELB

- Mix your health check types, an EC2 check goes well with ELB checks
- Be generous with your grace period
- Your data needs to fit on one machine. This design does not account for when sharding is necessary.


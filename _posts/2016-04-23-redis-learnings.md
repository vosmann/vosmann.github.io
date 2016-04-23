---
layout: post
title:  "Redis learnings"
date:   2016-04-23 19:00:00 +0100
categories: redis
---

## Planning the size of your Redis instance

<put into “design assumptions”?>
With an estimate of the top traffic the service gets, we can calculate the expected maximum amount of memory necessary to hold all the locks and recommendations data.

Some issues may arise with this approach. For example, the Redis cache could become too small if the traffic increases sufficiently. This could lead to items display not being able to create a single lock or to write a list.

## Learnings
Expire entries correctly and don’t leak memory

### Avoid evictions
Be wary of Redis’ approximated LRU algorithm. When using the least recently used eviction strategy, Redis does not choose the oldest entry to be evicted, as one might expect. It actually samples a small number of random entries, three by default, and simply evicts the oldest one.

In practice this means that an entry can get evicted moments after it was written. This would be about as bad as it can get in our use case.

I would recommend carefully reading the Redis documentation about its LRU eviction strategy.

Another thing worth considering is changing using the all-keys-lru strategy instead of the default volatile-lru. The latter only allows an entry to be if you will be coordinating multiple instances of your service with Redis is that your expire commands might not I am not very familiar with the Redis implementation of its default LRU eviction strategy. This algorithm assumes that Redis will respect expiry times set on keys. Even if this is not the case, for every the lock access, a list access had to have happened later, so LRU eviction should work as expected.

The volatile-lru eviction strategy only evicts volatile entries, i.e. ones on which an EXPIRE command was called. The all-keys-lru will evict even persistent ones (no EXPIRE).

.


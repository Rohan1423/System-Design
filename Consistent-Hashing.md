Consistent hashing is a technique used in distributed systems to minimize data reshuffling when nodes are added or removed. It’s widely used in systems like distributed caches (Redis clusters), CDNs, load balancers, and key-value stores.
Let’s build it up properly so it actually clicks.

1. The Problem Consistent Hashing Solves
Imagine you have a cache system with 3 servers:
S1
S2
S3
And you map data like this:
key → hash(key) % number_of_servers
So:
index = hash(key) % 3

-> What happens when a new server is added?
Now servers = 4.
That means:
index = hash(key) % 4

-> Problem:
Almost all keys get remapped.
So:
Cache becomes useless temporarily
Massive data migration happens
System load spikes
Same issue when a node fails.
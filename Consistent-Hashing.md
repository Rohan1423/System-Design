Consistent hashing is a technique used in distributed systems to minimize data reshuffling when nodes are added or removed. It’s widely used in systems like distributed caches (Redis clusters), CDNs, load balancers, and key-value stores.

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

2. Core Idea of Consistent Hashing

Instead of using modulo arithmetic, consistent hashing maps both:
Servers (nodes)
Keys (data)
onto a circular hash space (called a hash ring).

Think of a circle:
Hash values go from 0 → 2³² (or 0 → ∞ conceptually)
The end wraps back to the start (circle)

3. How It Works (Step by Step)

Step 1: Place servers on the ring
Each server is hashed:
hash(S1) → position 100
hash(S2) → position 400
hash(S3) → position 800

So they are placed on the ring.

Step 2: Place keys on the same ring
Each key is also hashed:
hash(K1) → 120
hash(K2) → 450
hash(K3) → 900

Step 3: Assignment rule
Each key is assigned to:
The first server clockwise from the key

Example:
K1 (120) → S2 (400)
K2 (450) → S3 (800)
K3 (900) → wraps around → S1 (100)

4. Why This is Powerful

-> When a server is added
Say we add S4 at position 500.
Only keys between:
S2 (400) → S4 (500)
get remapped.

-> Everything else stays unchanged.
So instead of rehashing everything:
Only ~1/n of keys move

-> When a server fails
If S2 dies:
Only keys assigned to S2 move to next server clockwise
Rest unaffected

5. The Real Problem: Uneven Distribution

If servers are randomly placed:
One server might get too many keys
Another might get very few
This is called load imbalance.

6. Solution: Virtual Nodes (VNodes)

Instead of placing each server once:
We place it multiple times on the ring:

S1 → S1a, S1b, S1c
S2 → S2a, S2b, S2c

Now:
Each server appears at multiple points
Distribution becomes much more uniform
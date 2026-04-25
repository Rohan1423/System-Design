-> What is Caching (in simple terms)?
Caching = storing frequently used data in a faster place so you can access it quickly later.
Instead of recomputing or fetching data again and again from a slow source (like a database), you store it somewhere fast (like memory).

-> Real-life analogy
Think of caching like this:
You order food from a restaurant → takes 30 minutes
Next time, instead of cooking again, you store leftovers in your fridge → takes 30 seconds
The fridge = cache
Cooking again = fetching from database

-> Why do we need caching?
Without caching:
Every request hits the database
Database becomes slow
System performance drops

With caching:
Faster response time
Reduced database load
Better scalability

-> How caching works (step-by-step)
User requests data (e.g., user profile)
System checks cache:
If data exists → return immediately (cache hit)
If not → fetch from DB (cache miss)
Store fetched data in cache for next time

-> Example (very important)
Imagine you're building a website:
Without cache
User → Server → Database → Server → User
With cache
User → Server → Cache → Server → User
                  ↓ (if miss)
               Database

-> Types of caching
1. In-Memory Cache

Stored in RAM (very fast)
Example:
Redis
Memcached
-> Used in backend systems

2. Browser Cache

Stored in user’s browser
Images, CSS, JS files
Reduces loading time for repeat visits

3. CDN Cache

Stored on global servers
Example:
Cloudflare
Akamai
-> Used for static content like images/videos

4. Database Cache

Some databases internally cache queries

-> Cache Hit vs Cache Miss
Cache Hit → Data found → FAST 
Cache Miss → Data not found → SLOW 
Goal: Increase cache hit ratio

-> Cache Eviction (very important)
Cache has limited space, so we must remove old data.

-> Common strategies:
LRU (Least Recently Used) → remove unused data
LFU (Least Frequently Used) → remove least used
TTL (Time To Live) → auto delete after time

-> Cache Invalidation (hardest part)
“There are only two hard things in Computer Science: cache invalidation and naming things.”
When data changes in DB, cache becomes outdated.

-> Example problem:
Cache: User name = "Rohan"
DB updated to "Rohan Sharma"
Cache still shows old value 

-> Solutions:
Update cache when DB updates
Use TTL (auto expiry)
Delete cache on update

-> Where caching is used (real systems)
Social media feeds
E-commerce product pages
API responses
Search results

-> When NOT to use caching
Avoid caching when:
Data changes very frequently
Real-time accuracy is critical (e.g., bank balance)

-> Simple code example (conceptual)

    if (cache.has(userId)) {
        return cache.get(userId); // fast
    } else {
        const data = db.getUser(userId); // slow
        cache.set(userId, data);
        return data;
    }
    
-> Summary
Caching is:
A performance optimization technique
Stores data temporarily in a fast storage layer
Reduces load on backend systems





-> Cache Invalidation Strategies

1. Time-based (TTL)

Cache expires after 5 minutes
Simple but may show stale data.

2. Write-through

Update cache + DB together:

sequenceDiagram
Client->>Server: Update Data
Server->>Database: Update
Server->>Cache: Update

3. Cache-aside (Most common)

sequenceDiagram
Client->>Server: Request
Server->>Cache: Check
Cache-->>Server: Miss
Server->>Database: Fetch
Server->>Cache: Store
Server->>Client: Response

On update:
Invalidate cache

4. Write-back (advanced)
Write to cache first
Sync to DB later
Used in high-performance systems.





-> Cache Eviction

-> Problem
Cache has limited memory.
When full → which data to remove?

-> Policies

-> LRU (Least Recently Used)
Remove item not used for longest time.
-> Example
Cache: A B C D
Access: A, B
Evict → C (least recently used)

-> LFU (Least Frequently Used)
Remove item used least times.
-> Example
A (used 10 times)
B (used 2 times)
C (used 1 time)
Evict → C

-> LRU vs LFU
Policy	        Based On
LRU	            Last used time
LFU	            Usage frequency

-> Real-world
Redis uses LRU (by default variants)
LFU used in recommendation systems





-> CDN (Content Delivery Network)

-> What is CDN?
A globally distributed cache system
Stores static content closer to users.

-> Without CDN
UserIndia --> ServerUS
UserIndia --> ServerUS
High latency

-> With CDN
UserIndia --> CDNIndia
CDNIndia --> ServerUS

-> Flow
User requests image
CDN checks local cache
If found → return fast
If not → fetch from origin server

-> Benefits
Low latency
Faster loading
Reduced server load
Global scalability

-> Example
When you open:
Netflix
YouTube
Videos are served from nearest CDN.

-> Types of Caching (Interview Bonus)
Type	            Example
Client cache	    Browser
CDN cache	        Cloudflare
Server cache	    Redis
DB cache	        Query cache
What is Caching (in simple terms)?

Caching = storing frequently used data in a faster place so you can access it quickly later.

Instead of recomputing or fetching data again and again from a slow source (like a database), you store it somewhere fast (like memory).

🔹 Real-life analogy

Think of caching like this:

You order food from a restaurant → takes 30 minutes
Next time, instead of cooking again, you store leftovers in your fridge → takes 30 seconds

👉 The fridge = cache
👉 Cooking again = fetching from database

🔹 Why do we need caching?

Without caching:

Every request hits the database
Database becomes slow
System performance drops

With caching:
Faster response time ⚡
Reduced database load 📉
Better scalability 📈

🔹 How caching works (step-by-step)
User requests data (e.g., user profile)
System checks cache:
✅ If data exists → return immediately (cache hit)
❌ If not → fetch from DB (cache miss)
Store fetched data in cache for next time

🔹 Example (very important)

Imagine you're building a website:

Without cache
User → Server → Database → Server → User
With cache
User → Server → Cache → Server → User
                  ↓ (if miss)
               Database
🔹 Types of caching
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
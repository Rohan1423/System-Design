==> What is NoSQL?
NoSQL = Non-relational databases designed for scale, flexibility, and high performance

Unlike SQL:
No fixed schema
Designed for distributed systems
Scales horizontally

-> Why NoSQL Exists?
Problems with SQL at scale:
Hard to scale horizontally
Strict schema
Joins become expensive

-> So NoSQL trades: Consistency → for → Scalability & Performance


-> What “Consistency” means
In databases, consistency means: Every user always sees the latest, correct data

-> Example:
You update your profile name to "Rohan"
Immediately, everyone (and every server) sees "Rohan" — no old values

-> What “Scalability & Performance” means
Scalability → system can handle more users by adding more servers
Performance → fast reads/writes (low latency)

-> The Trade-off (Why NoSQL sacrifices consistency)
NoSQL databases (like MongoDB or Redis) are designed to run on many distributed servers.

-> Now imagine:
You have 10 servers across the world
You update data on 1 server

To keep perfect consistency, all 10 servers must:
sync immediately
confirm the update

-> This slows things down a lot

-> What NoSQL does instead
NoSQL says: “Let’s relax consistency a bit so we can go faster and scale better”

So:
Data may take time to sync across servers
Some users might temporarily see old data
This is called: Eventual Consistency

-> Real-world example:
Think of Instagram:
You like a post
Your friend might not see that like immediately
After a few seconds → it appears
Slight inconsistency, but super fast app

-> “NoSQL trades Consistency for Scalability & Performance” means:
It gives up instant accurate data everywhere

-> In return, it gains:
Faster responses
Ability to handle millions of users
Easy horizontal scaling





==> Types of NoSQL Databases
1) Key-Value Store (Example: Redis)
Data stored as: key → value

-> Example
"user:101" → "Rohan"
"cart:101" → ["item1", "item2"]

-> Key = unique identifier
-> Value = actual data (can be string, number, JSON, etc.)

-> Use Cases
Caching
Sessions
Rate limiting
Leaderboards

-> Diagram

App --> Redis
Redis --> Key1["user:101"]
Redis --> Key2["cart:101"]

-> Why Fast?
In-memory
O(1) lookup

-> Limitations
No complex queries
No joins





==> What is Redis?

Redis is:
An in-memory key-value database
Extremely fast
Often used as a cache, session store, or real-time data store

-> Why fast?
Because it stores data in RAM, not on disk.

-> What “stored in RAM” actually means
When we say Redis stores data in RAM, it means: Your data is kept directly in the computer’s main memory, not saved in files on the hard drive.

-> How It Works Internally

Traditional DB (like MySQL):
Data stored on disk
Slower reads/writes

Redis:
Data stored in memory (RAM)
Access time ≈ microseconds

-> That’s why Redis is used when speed matters.

-> Data Types in Redis
Unlike simple key-value stores, Redis supports rich data structures:

1. String (most common)
SET name "Rohan"
GET name

2. List (like array)
LPUSH tasks "task1"
LPUSH tasks "task2"

3. Hash (like object)
HSET user:101 name "Rohan" age 25
HGET user:101 name

4. Set (unique values)
SADD tags "redis" "database"

5. Sorted Set (ranking system)
ZADD leaderboard 100 "player1"

-> Used for:
Leaderboards
Ranking systems

-> Why Redis is So Fast

1. In-memory storage
No disk I/O → huge speed gain

2. Simple operations
No joins, no complex queries

3. Single-threaded design
No locking issues
Very efficient execution

-> Common Use Cases (VERY IMPORTANT)

1. Caching (Most common)
Instead of hitting DB:
App → Redis → (if miss) → DB
-> Example:
Store API response
Reduce DB load

2. Session Storage
session:abc123 → user data
Used in:
Login systems
Authentication

3. Real-time Analytics
Page views
Counters
INCR page_views

4. Leaderboards
Using sorted sets

5. Rate Limiting
Example:
Allow only 100 requests/min

-> TTL (Time To Live)

Redis allows auto-expiry:
SET otp "123456" EX 60
After 60 seconds → deleted automatically

Used for:
OTPs
Sessions
Cache expiry

-> Advantages
Extremely Fast: Microsecond latency
Simple Model: Easy to understand
Flexible Data Types: Not just plain key-value
Built-in Expiry: TTL support

-> Disadvantages
Data Loss Risk: Stored in RAM, Can lose data on crash (unless persistence enabled)
Limited Querying: No joins, No complex queries
Memory is Expensive: RAM costs more than disk

-> Redis vs Traditional SQL
Feature	      Redis	              SQL (MySQL)
Storage   	  RAM	                Disk
Speed	        Very Fast	          Slower
Querying	    Simple	            Complex (joins)
Scalability	  Easy	              Moderate
Use case	    Cache, realtime	    Transactions

-> When Should You Use Redis?
Use Redis when:
You need high speed
Data is temporary
You need real-time updates

-> Examples:
Caching API responses
Sessions
Counters
Notifications

-> When NOT to Use Redis
Avoid if:
You need complex queries
Data must be 100% durable
You need relationships (joins)

-> Real System Design Example

Without Redis:
User → Backend → Database (slow)

With Redis:
User → Backend → Redis (fast)
                  ↓ (miss)
                Database

-> This is called Cache Aside Pattern

-> Think of Redis like: "Your app’s short-term memory (fast but temporary)"

And SQL DB like: "Your long-term storage (slower but permanent)"





2) Document Database (Example: MongoDB)

Stores data as JSON-like documents.

-> Example
{
  "user_id": 101,
  "name": "Rohan",
  "orders": [
    { "order_id": 1, "amount": 500 },
    { "order_id": 2, "amount": 300 }
  ]
}

-> Diagram
App --> MongoDB
MongoDB --> Doc1["User Document"]
MongoDB --> Doc2["Product Document"]

-> Use Cases
User profiles
Product catalogs
Content management
Flexible schema apps

-> Advantages
Flexible schema
Easy to scale
Nested data (no joins)

-> Limitations
Data duplication
Hard to maintain consistency





3 Column Database (Wide Column)

-> Examples:
Cassandra
HBase

Stores data by columns instead of rows.

-> Example

UserID | Name | Order1 | Order2 | Order3
101    | Rohan| 500    | 300    | 200

Optimized for: Large-scale reads & writes

-> Diagram
App --> ColumnDB
ColumnDB --> Row1
ColumnDB --> Row2

-> Use Cases
Time-series data
Analytics
Logging systems
High write systems

-> Advantages
Massive scalability
High throughput
Good for big data

-> Limitations
Complex queries are hard
Not ideal for transactions
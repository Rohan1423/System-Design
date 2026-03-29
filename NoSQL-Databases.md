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
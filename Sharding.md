-> Sharding is one of the most important database scaling topics.

-> A common interview progression is:
Single Database
↓
Replication
↓
Read Replicas
↓
Database Still Too Large
↓
Sharding


-> Imagine you have a database with 1 billion users.

-> Initially:
Database Server
Users Table
1 billion rows
Everything is stored on one machine.

-> As traffic grows:
Queries become slower
Storage becomes full
CPU becomes overloaded
RAM becomes insufficient
At some point, vertical scaling (adding more CPU/RAM) is no longer enough.
This is where Sharding comes in.

-> What is Sharding?

Sharding = Splitting data across multiple databases/servers.
Instead of:

1 Server
┌─────────────┐
│ All Users   │
└─────────────┘

-> You do:

Server A      Server B      Server C
┌───────┐     ┌───────┐     ┌───────┐
│Users  │     │Users  │     │Users  │
│1-100M │     │100-200│     │200-300│
└───────┘     └───────┘     └───────┘

Each server stores only a portion of the data.
These portions are called shards.


-> Why Do We Need Sharding?

-> Suppose:
Users Table = 2 TB
But one database server can comfortably handle:
500 GB
Not enough.

-> Instead:
Shard 1 = 500 GB
Shard 2 = 500 GB
Shard 3 = 500 GB
Shard 4 = 500 GB
Now storage is distributed.

-> Real World Example

Think of a library.

-> Without sharding:
One huge room
10 million books
Finding books becomes difficult.

-> With sharding:
Room A -> A-F
Room B -> G-M
Room C -> N-S
Room D -> T-Z
Each room stores only part of the books.
Searching becomes easier.


-> How Sharding Works

-> Suppose we have:
Users
------
UserID
Name
Email

-> Data:
1
2
3
4
5
6
7
8

-> Three shards:
Shard 1
Shard 2
Shard 3

-> We need a rule deciding:
Which user goes where?
This rule is called a Shard Key.


-> What is a Shard Key?

A shard key is the field used to determine which shard stores a record.

-> Example:
UserID
Then:
UserID → Shard

-> Method 1: Range-Based Sharding
Store ranges on different servers.

Shard 1:
UserID 1 - 1000

Shard 2:
UserID 1001 - 2000

Shard 3:
UserID 2001 - 3000

-> Example:
UserID 500
goes to:
Shard 1

-> Visualization

Shard 1
1 - 1000

Shard 2
1001 - 2000

Shard 3
2001 - 3000

Simple.
Easy to understand.


-> Problem with Range Sharding

Imagine new users always get increasing IDs.
2999
3000
3001
3002
3003
3004

-> All new writes go to:
Shard 3

-> Result:
Shard 1 -> Idle
Shard 2 -> Idle
Shard 3 -> Overloaded

-> This is called a Hotspot.


-> Hotspot Problem
A hotspot occurs when:
One shard receives most traffic

-> Example:
Shard 1 -> 10%
Shard 2 -> 15%
Shard 3 -> 75%

One server becomes overloaded.
Others sit idle.
Bad utilization.


-> Method 2: Hash-Based Sharding

-> Instead of ranges:
hash(UserID)
decides the shard.

-> Example:
Shard = UserID % 3
Example
UserID:
1 % 3 = 1
→ Shard 1

2 % 3 = 2
→ Shard 2

3 % 3 = 0
→ Shard 3

4 % 3 = 1
→ Shard 1

Result:
Shard 1:
1 4 7 10

Shard 2:
2 5 8 11

Shard 3:
3 6 9 12
Much more balanced.


-> Visualization

Users
1 -> S1
2 -> S2
3 -> S3
4 -> S1
5 -> S2
6 -> S3
Load spreads evenly.


-> Advantage of Hash Sharding

-> Traffic becomes:
Shard 1 -> 33%
Shard 2 -> 33%
Shard 3 -> 34%
Balanced.
No hotspot.

-> Problem with Hash Sharding

-> Suppose:
3 shards

-> Formula:
UserID % 3
Now add:
Shard 4

-> Formula changes:
UserID % 4
Every mapping changes.

-> Example:
5 % 3 = 2
Old:
Shard 2
New:
5 % 4 = 1

-> Now:
Shard 1
Almost all data must move.
Huge problem.
This is why systems often use Consistent Hashing.


-> Method 3: Directory-Based Sharding

Maintain a lookup table.
UserID → Shard

-> Example:
User 1 -> Shard 2
User 2 -> Shard 1
User 3 -> Shard 4
Stored separately.

-> Visualization

Routing Table
1 -> S2
2 -> S1
3 -> S4
4 -> S3
Database checks the table first.
Then goes to the correct shard.

-> Pros
Flexible.
Can move users between shards.

-> Cons
Need extra lookup.
Routing table becomes critical.

-> If it fails:
Nobody knows where data lives.


-> Query Flow in Sharding

-> Suppose:
Get User 1500

-> Application:
Determine shard

-> Then:
Read shard

-> Example:
1500
belongs to: Shard 2
Only Shard 2 is queried.
Very efficient.


-> What Happens During Writes?

Insert User 4500
Router computes: hash(4500)
Determines: Shard 3
Stores data there.
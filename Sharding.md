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
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
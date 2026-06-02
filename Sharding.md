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

Initially:
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

You do:

Server A      Server B      Server C
┌───────┐     ┌───────┐     ┌───────┐
│Users  │     │Users  │     │Users  │
│1-100M │     │100-200│     │200-300│
└───────┘     └───────┘     └───────┘

Each server stores only a portion of the data.
These portions are called shards.
-> Replication is used everywhere:
Databases
Caches
Distributed systems
Global applications

1. What is Replication?

Replication = Copying data across multiple servers

-> Why Needed?

Without replication:
Users --> Database
If DB crashes
→ entire system down

-> With Replication
Users --> DB1
DB1 --> DB2
DB1 --> DB3

Now:
Backup copies exist
High availability
Better read scaling
Disaster recovery

2. Leader-Follower Replication

-> Also called:
Master-Slave
Primary-Replica

-> Idea
One server handles writes.
Followers copy data from leader.

-> Architecture
Client --> Leader
Leader --> Follower1
Leader --> Follower2

-> Write Flow
sequenceDiagram
Client->>Leader: Write Request
Leader->>Follower1: Replicate
Leader->>Follower2: Replicate
Leader-->>Client: Success

-> Read Flow

Reads may go to replicas:
Client --> Follower1
Client --> Follower2

-> Advantages
Simple
High read scalability
Good consistency control

-> Problems
Leader becomes bottleneck
All writes go to one server.
Replication Lag
Follower may not immediately receive latest data.

Example:
Leader → ₹500
Follower → still ₹1000

This creates eventual consistency.

3. Read Replica

-> What is it?
Follower servers dedicated for reads.

-> Example
Users --> App
App --> Leader["Leader (Writes)"]
App --> Replica1["Read Replica"]
App --> Replica2["Read Replica"]

-> Why Important?

-> Massive apps have:
Few writes
Huge reads

-> Example:
Instagram feed browsing
YouTube video metadata

-> Benefits
Reduces leader load
Scales reads horizontally
Improves latency

-> Limitation
Replica may be stale.

4. Multi-Leader Replication

-> Now instead of one leader:
Multiple leaders accept writes.

-> Architecture
Client1 --> LeaderA
Client2 --> LeaderB
LeaderA --> LeaderB
LeaderB --> LeaderA

-> Why Use It?
Useful for:
Multi-region systems
Global applications

-> Example:
India users → India leader
US users → US leader
Low latency globally.

-> Advantages
Faster regional writes
No single write bottleneck
Better availability

-> Biggest Problem: Conflict Resolution

-> Example:
Leader A → Name = "Rohan"
Leader B → Name = "Rahul"
Now which is correct?
This is hard.

-> Conflict Resolution Strategies
Last write wins
Version vectors
CRDTs (advanced)
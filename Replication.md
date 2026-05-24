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
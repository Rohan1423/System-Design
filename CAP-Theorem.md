What is CAP Theorem?

In a distributed system, you can only guarantee 2 out of 3:

C → Consistency
A → Availability
P → Partition Tolerance

-> First Understand “Partition”
Partition = Network failure between nodes

Example:
ServerA <--X--> ServerB

Meaning:
Servers cannot talk to each other
Network is broken

-> This WILL happen in real systems

-> So: Partition Tolerance is NOT optional in distributed systems.

-> So CAP really becomes:
You must choose between:
Consistency
Availability
WHEN partition happens


1) Consistency (C)

-> Meaning
All nodes show the same data at the same time

-> Example
User updates balance:
Server A → ₹1000 → ₹500
Server B → must also immediately show ₹500
No stale data allowed.

-> Diagram
Client --> ServerA
Client --> ServerB
ServerA -->|Updated: 500| ServerB

-> Pros
Always correct data
No confusion

-> Cons
Slower system
May block requests

2) Availability (A)

-> Meaning
System always responds, even if data is not latest

-> Example
If Server B is outdated:
Server B still responds: ₹1000
Even if it's slightly wrong → it still responds

-> Diagram
Client --> ServerA
Client --> ServerB
ServerB --> Response["Old Data (Still responds)"]

-> Pros
Always responds
Fast system
No downtime

-> Cons
May return stale data

3) Partition Tolerance (P)

-> Meaning
System continues working even if network fails between nodes

-> Example
Servers cannot communicate:
Server A ❌ Server B
System must still operate somehow.

-> Diagram
A --> X
X --> B

-> The CAP Tradeoff
When partition happens:
Choice	        Result
CP	            Correct data, possible downtime
AP	            Always available, maybe stale data
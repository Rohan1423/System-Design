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
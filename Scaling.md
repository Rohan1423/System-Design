1 What is Scaling?
Scaling = Ability of a system to handle increasing load (users, traffic, data)

-> Example:
1,000 users → works fine
1,000,000 users → system crashes

-> Scaling ensures it still works





2 Vertical Scaling (Scale Up)

-> Definition
Increase the power of a single machine
More CPU
More RAM
Better disk

-> Diagram
Users --> Server
Server --> BiggerCPU
Server --> MoreRAM
Server --> FasterDisk

-> Example

You upgrade:
8 GB RAM → 64 GB RAM
4 CPU → 32 CPU
Same server, more powerful.

-> Advantages
Simple
No code changes
Easy to manage

-> Limitations
Hardware limit exists
Expensive
Single point of failure

-> Real-World
Early-stage apps or startups often use vertical scaling first.





3 Horizontal Scaling (Scale Out)

-> Definitin
Add more machines instead of increasing one machine

-> Diagram
Users --> LoadBalancer
LoadBalancer --> Server1
LoadBalancer --> Server2
LoadBalancer --> Server3

-> Example
Instead of 1 server:
1 server → 1000 users
10 servers → 10,000 users

-> Advantages
Handles massive scale
Fault tolerant
Flexible

-> Challenges
Needs load balancer
Data consistency issues
Complex architecture

-> Real-World
Companies like:
Netflix
Amazon
Use horizontal scaling.



-> Vertical vs Horizontal
Feature	        Vertical	            Horizontal
Scaling type	Upgrade machine	        Add machines
Complexity	    Low	                    High
Limit	        Hardware limit	        Almost unlimited
Cost	        Expensive long-term	    More flexible
Failure	        Single point failure	Fault tolerant
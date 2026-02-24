HLD vs LLD

🔷 High-Level Design (HLD)

What it is:
Bird's eye view of the system

It focuses on:
-> Major Componenets
-> Architecture
-> Data Flow
-> Scaling Strategies
-> Technology Choices

Example: Design Instagram (HLD)
-> Client (Mobile App)
-> API Gateway
-> Application Servers
-> Cache
-> Database
-> CDN
-> Load Balancer

We don't talk about Classes or Code here

Example: Social Media App (HLD)

Client --> LoadBalancer
LoadBalancer --> APIServer1
LoadBalancer --> APIServer2
APIServer1 --> Cache
APIServer2 --> Cache
Cache --> Database
APIServer1 --> CDN
APIServer2 --> CDN


What this shows:
-> Major component
-> Traffic flow
-> Scaling strategy
-> No internal class details





🔷 Low-Level Design (LLD)

What it is:
Detailed Internal Design of Componenets

It focuses on:
-> Classes
-> Methods
-> Database Schema
-> Design Pattern
-> Edge Cases

Example: Design Parking Lot (LLD)
-> Class Vehicle
-> Class ParkingSpot
-> Class Ticket
-> Enum VehicleType
-> Methods like parkVehicle(), unparkVehicle()


Example: Parking Lot System (LLD)

class Vehicle {
  +String licenseNumber
  +VehicleType type
}

class ParkingSpot {
  +int spotNumber
  +VehicleType type
  +isOccupied()
}

class Ticket {
  +String ticketId
  +Date entryTime
  +Date exitTime
}

Vehicle --> Ticket
ParkingSpot --> Vehicle


What this shows:
-> Classes
-> Attributes
-> Relationships




Key Difference:

   HLD	                                LLD

-> Big                                  picture	Internal details
-> Architecture	                        Code structure
-> Scaling	                            OOP design
-> Used in System Design round	        Used in LLD / Machine coding round








Functional vs Non-Functional Requirements

🔷 Functional Requirements

-> It is what system should do

Example: Design Whatsapp

Functional Requirements:
-> User can send messages
-> User can receive messages
-> User can see online status

These are features.





🔷 Non-Functional Requirements

-> How system should behave

==> These include:

-> Scalability: Ability of the system to handle increasing load.
Example: Your chat app initially supports 1 million users.Now it grows to 100 million users.

==> If the system: 
-> Adds more servers
-> Distributes traffic using load balancer
-> Scales database via sharding
-> And still works smoothly → it is scalable.

Example Statement: "System should support 100M users and 10M concurrent connections."
-> As users increase → add more servers.



-> Availability: System should be accessible and operational whenever users need it.
==> Measured in uptime:
-> 99%
-> 99.9%
-> 99.99%
Example: If one server crashes, users should still be able to send messages.

Example Statement: "System should have 99.99% uptime."
-> This means downtime per year ≈ 52 minutes only.
==> If:
-> Server1 fails → Server2 works
-> PrimaryDB fails → ReplicaDB takes over
System remains available.



-> Latency: Time taken for a request to travel from client → server → client.
==> Measured in milliseconds (ms).
Example:
-> User sends a message.
-> If message delivery takes:
-> 50ms → Excellent
-> 200ms → Acceptable
-> 3 seconds → Bad UX

Example Statement: "Message delivery latency should be < 200ms."
-> Total time from User1 → User2 should be < 200ms.
Low latency = good user experience.



-> Security: System should protect data from unauthorized access.
Example:
-> In a chat app:
-> Messages should be encrypted.
-> Only sender & receiver can read.

-> If hacker intercepts traffic → data should still be unreadable.

Example Statement: "Messages must be end-to-end encrypted."
==> Add:
-> HTTPS
-> JWT authentication
-> Encryption
Security protects confidentiality.



-> Reliability: System should perform correctly and not lose data.Even during failures.
Example:
-> User sends a message.
-> Even if:
-> Server crashes
-> Network drops
-> Message should NOT be lost.
==> It should:
-> Retry
-> Be stored safely
Eventually delivered

Example Statement: "Messages must not be lost."
==> Using:
-> Message queues
-> Persistent storage
-> Retry mechanism
Ensures reliability.



-> Performance: Overall efficiency of the system under load.
==> Includes:
-> Response time
-> Throughput: Number of requests the system can handle per unit time.
Measured as:
-> Requests per second (RPS)
-> Transactions per second (TPS)
-> Messages per second
-> It measures capacity.

Suppose:
-> 1 million users online
-> Each sends 1 message every 10 seconds

==> That means:
-> 1,000,000 / 10 = 100,000 messages per second

==> So your system must support:
-> 100K messages per second throughput
-> If it can only handle 20K messages/sec → system will lag or crash.


-> Resource usage: Multiple users or services share the same system resources like:
-> CPU
-> Memory
-> Database
-> Network
-> Storage
Efficient sharing ensures system remains stable.

Example: Database Shared by Multiple Services
=> Imagine:
-> User Service
-> Order Service
-> Payment Service
All using the same database.

=>Problem:
-> If Order Service suddenly generates heavy traffic,
-> Database CPU spikes → other services slow down.
This is resource contention.

=> Use:
-> Separate DB instances
-> Kubernetes resource limits
-> Rate limiting
-> Auto-scaling

Example:
-> If 1 million users send messages at the same time:
-> System should not slow down drastically
-> CPU & memory usage should remain optimized

Example Statement: "System should handle 50,000 requests per second."
==> Using:
-> Caching
-> Load balancing
-> Efficient DB indexing
Improves performance.


What scale are we targeting?
-> That moves discussion from functional → non-functional.









Monolith vs Microservices

🔷 Monolith Architecture

-> All components inside one application.

Example:
-> Single codebase
-> Single deployment
-> Single database

Advantages:
-> Simple
-> Easy to develop initially
-> Good for small teams

==> Problems:
-> Hard to scale parts independently
-> Hard to deploy large apps
-> One bug can crash entire system

Example:
Early stage startups.





🔷 Microservices Architecture

->Application split into small independent services.

Example:
-> Instagram:
-> User Service
-> Post Service
-> Feed Service
-> Notification Service
==> Each service:
-> Has own database
-> Deployed independently
-> Scales independently

==> Advantages:
-> Independent scaling
-> Fault isolation
-> Faster deployment

Problems:
-> Complex
-> Network overhead
-> Hard debugging
-> Distributed failures




Startups → Monolith
Large scale companies → Microservices

==>But:
->Monolith is not bad.
->Microservices is not always better.

It depends on scale.
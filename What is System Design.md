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

-> HLD	                                LLD
-> Big                                 picture	Internal details
-> Architecture	                    Code structure
-> Scaling	                            OOP design
-> Used in System Design round	        Used in LLD / Machine coding round
-> Load Balancer
A load balancer is a system (hardware or software) that distributes incoming network traffic across multiple servers so that no single server gets overloaded.

-> Instead of one server handling all users:
A load balancer sits in front
It forwards each request to one of many servers
This keeps the system fast and reliable

-> Example
Imagine you have 3 app servers:
Server A
Server B
Server C

-> Without load balancer:
All users hit Server A → it becomes slow/crashes

With load balancer:
User 1 → Server A
User 2 → Server B
User 3 → Server C
Next user → back to A (or based on rules)

-> Why it is used
1. High Availability

If one server fails, traffic goes to others.

2. Better Performance

Traffic is shared evenly.

3. Scalability

You can add more servers easily.

4. No single point of failure

System stays up even if one machine crashes.

-> Common Load Balancing Methods
Round Robin → one by one in order
Least Connections → sends traffic to least busy server
IP Hash → same user goes to same server
Weighted Routing → powerful servers get more traffic

-> Where it is used
Websites (Amazon, Netflix, etc.)
APIs / microservices
Cloud systems (AWS, Azure, GCP)
Gaming servers

-> Real-world tools
NGINX (also used as load balancer)
HAProxy
Amazon Web Services Elastic Load Balancer (ELB)





-> Why Do We Need a Load Balancer?

-> Problem Without Load Balancer

All users hit one server:
Users --> Server1

-> Problems:
Server overload → crash
Slow response
No scalability
Single point of failure

-> Solution: Load Balancer

Distributes traffic across multiple servers:
Users --> LoadBalancer
LoadBalancer --> Server1
LoadBalancer --> Server2
LoadBalancer --> Server3

-> Why It’s Needed

A Load Balancer helps:
Distribute traffic evenly
Improve availability
Increase scalability
Handle failures (health checks)
Prevent server overload





Types of Load Balancers

-> L4 Load Balancer (Layer 4 - Transport Layer)

Works on:
IP address
TCP/UDP port

Cannot see:
URL (/api/users)
Headers
Cookies

-> L4 Diagram
Client --> L4LB
L4LB --> Server1
L4LB --> Server2

-> Example
Routing based on:
IP + Port only
So request goes blindly to a server.

-> Pros:
Very fast
Low latency
Simple

-> Cons:
No smart routing
No path-based decisions

-> L7 Load Balancer (Layer 7 - Application Layer)

Works on:
HTTP/HTTPS
URL path
Headers
Cookies

-> L7 Diagram
Client --> L7LB
L7LB -->|/users| UserService
L7LB -->|/orders| OrderService
L7LB -->|/payments| PaymentService

-> Example
Requests:
/api/users → User Service
/api/orders → Order Service

-> Pros:
Smart routing
API-based routing
Supports microservices

-> Cons:
Slower than L4
More CPU overhead

-> L4 vs L7
Feature	        L4	        L7
Layer	        Transport	Application
Data visibility	IP/Port	    Full HTTP
Routing	        Basic	    Intelligent
Speed	        Faster	    Slower
Use case	    TCP apps	Web apps





-> Load Balancing Algorithms

1. Round Robin
Concept:
Requests are distributed one by one in order.

-> Diagram
User1 --> Server1
User2 --> Server2
User3 --> Server3
User4 --> Server1

-> Example:
Request 1 → Server A  
Request 2 → Server B  
Request 3 → Server C  
Request 4 → Server A

-> Pros:
Simple
Fair distribution

-> Cons:
Doesn't consider server load
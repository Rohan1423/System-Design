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
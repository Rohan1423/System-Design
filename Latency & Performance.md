==> Latency

Latency = Time taken for a single request to get a response.

Example:

You open Google.
Request → Server → Response
If it takes 120 ms, then:
-> Latency = 120 ms

-> Example
Login API:

User clicks login
Response received in 150ms

-> So: Latency = 150 ms

-> Good systems aim for:
API latency: <200 ms
Page load: <2 seconds





==> Throughput

-> Throughput = Number of requests processed per second.

-> Measured as:
Requests per second (RPS)
Transactions per second (TPS)


Example:
If a server handles:
5000 requests per second

-> Then:
Throughput = 5000 RPS


Example:
Suppose 1 million users
Each sends 1 request every 10 seconds

-> Calculation:
1,000,000 / 10
= 100,000 RPS

So system must support:
-> 100k requests per second





==> BandWidth

-> BandWidth = Maximum amount of data that can be transferred per second.

-> Measured in:
   Mbps
   Gbps


-> Example:
If a network supports 1 Gbps
That means it can transfer 1 gigabit of data per second.


-> Example:
Suppose video size = 5 MB
If bandwidth allows:
100 MB per second
Then you can stream:
100 / 5 = 20 videos per second
Bandwidth limits how much data flows.





==> Availability

Availability = Percentage of time a system is operational.

Formula: Availability = Uptime / Total Time


-> Example:
If system runs 364 days out of 365
Availability: 364 / 365 = 99.73%


-> Common Availability Targets:
Availability	    Downtime per year
99%	                ~3.6 days
99.9%	            ~8.7 hours
99.99%	            ~52 minutes
99.999%	            ~5 minutes

-> Large companies like Amazon Web Services target 99.99% or higher.
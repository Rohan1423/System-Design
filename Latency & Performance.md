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
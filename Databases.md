==> What is a Database?
A database is simply an organized way to store, manage and retrive data efficiently.

-> Think of it like a smart digital storage system where you can:
Save data
Search data quickly
Update/delete data safely
Handle large-scale applications


-> Types of Databases:

1) SQL Databases (Relational)
Example:
MySQL
PostgreSQL
Oracle Database

-> Features:
Data stored in tables
Uses SQL (Structured Query Language)
Strong consistency (ACID)

-> Best for:
Banking
E-commerce orders
Transactions


2) NoSQL Databases (Non-relational)
Examples:
MongoDB
Cassandra
Redis

-> Features:
Flexible schema
Scales horizontally
Faster for large distributed systems

-> Best for:
Real-time apps
Big data
Caching


-> What a Database Does Internally
A database system:
Stores data on disk
Uses indexes for fast lookup
Manages concurrent users
Ensures ACID properties
Recovers data after crashes

-> Database vs DBMS
Database → The actual data
DBMS (Database Management System) → Software managing it

-> Examples of DBMS:
MySQL
PostgreSQL

-> Real-World Use
Every major app uses databases:
Instagram → stores posts, users
Amazon → orders, products
Banking apps → transactions


-> When someone says “database”, they are thinking:
How do you:
Store data efficiently?
Query fast?
Scale to millions of users?
Keep data consistent?





1. SQL Databases (Relational Databases)

-> Examples: MySQL, PostgreSQL
-> Data is stored in tables (rows + columns) with a fixed schema.

-> Example:
Users(id, name, email)
Orders(id, user_id, amount)

-> Tables are related using keys (foreign key relationships)

-> How SQL DBs Work Internally

1. Storage
Data stored in pages (blocks) on disk
Organized using B-Trees for indexing

2. Query Execution
When you run:
SELECT * FROM Users WHERE email = 'a@gmail.com';

Steps:
Query parser
Query optimizer (chooses best plan)
Uses index (if exists)
Fetches data

3. Transactions (ACID)
SQL DBs strictly follow ACID
Uses Write-Ahead Logging (WAL)
Ensures crash recovery

-> Relationships
Supports:
One-to-One
One-to-Many
Many-to-Many

Using:
Foreign Keys
Joins


-> Strengths:
Strong Consistency
Always correct data
Complex Queries
JOIN, GROUP BY, aggregation
Data Integrity
Constraints (PRIMARY KEY, UNIQUE, NOT NULL)


-> Weaknesses
Scaling is hard
Vertical scaling (bigger machine)
Schema rigidity
Hard to change structure


-> Real Use Cases
Use SQL when:
Payments (banking systems)
Orders (e-commerce)
Inventory systems

-> Anywhere correctness > speed





2) NoSQL Databases (Non-Relational)

-> Examples: MongoDB, Cassandra, Redis
-> No fixed schema + designed for scale and flexibility

-> Types of NoSQL
1. Document DB (Most common)

-> Example: MongoDB

{
  "user_id": 1,
  "name": "Rohan",
  "orders": [
    { "id": 101, "amount": 2000 }
  ]
}

-> Nested JSON-like structure

2. Key-Value Store
-> Example: Redis
"user:1" → {name: "Rohan"}
-> Extremely fast (O(1))

3. Wide Column DB
-> Example: Cassandra
-> Used for massive scale (billions of rows)

4. Graph DB (less common in interviews)
Social networks
Relationships-heavy queries

-> How NoSQL Works Internally
1. Distributed by default
Data split across machines (sharding)

2. Replication
Copies data across nodes

3. Eventual Consistency
Based on CAP Theorem

You trade:
Consistency
Availability
Partition tolerance

-> NoSQL often chooses:
Availability + Partition tolerance

-> Strengths
Horizontal scaling
Add more servers easily
Flexible schema
No strict structure
High performance

Optimized for specific use cases

-> Weaknesses
Weak consistency (sometimes)
Data may be temporarily inconsistent
No joins (mostly)
Data duplication required

-> Real Use Cases
Chat apps (messages)
Analytics systems
Social media feeds
Caching (Redis)





3. SQL vs NoSQL (Key Differences)
-> Data Model
SQL	            NoSQL
Tables	        JSON / Key-Value
Fixed schema	Flexible schema

-> Scalability
SQL	            NoSQL
Vertical	    Horizontal

-> Consistency
SQL	            NoSQL
Strong (ACID)	Eventual
-> Relationships

SQL             NoSQL
Supports JOIN	Avoid JOIN

-> Performance
SQL	            NoSQL
Complex queries	High-speed simple queries





=> ACID Properties
ACID ensures reliable database transactions.


A → Atomicity
All or nothing

Example:
User places order
Payment deducted
Order created

If payment succeeds but order fails → rollback everything


C → Consistency
Data remains valid

Example:
Bank balance cannot go negative
Order must have a valid user_id


I → Isolation
Transactions don’t interfere

Example:
Two users buying last item
Only one should succeed


D → Durability
Once saved, always saved
Even if server crashes → data remains (disk persistence)
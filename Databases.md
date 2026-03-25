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





==> What is Indexing

An index in a database is just like the index at the back of a book:
Instead of reading the whole book, you jump directly to the page.

In databases:
Without index → scan everything (slow)
With index → jump directly (fast)

-> Internal Idea (How DB actually stores it)
Most databases (like MySQL, PostgreSQL) use:
-> B-Tree
This is a sorted tree structure that allows:
Fast search: O(log n)
Instead of: O(n)

-> Example Table (Large Scale)

Imagine:
orders table (1 million rows)
order_id | user_id
1        | 101
2        | 102
3        | 103
...
1000000  | 999

-> Case 1: WITHOUT Index

Query:
SELECT * FROM orders WHERE user_id = 101;
What DB does internally:
Start from row 1
Check user_id → not match
Row 2 → not match
Row 3 → not match
...
Until it finds user_id = 101

-> This is called: Full Table Scan

Complexity:
Time: O(n)
For 1M rows → checks almost all rows

-> Case 2: WITH Index

Now create index:
CREATE INDEX idx_user_id ON orders(user_id);
Internally DB builds something like:
Index (sorted):

user_id → pointer to row
101 → row 1
102 → row 2
103 → row 3
...

-> Actually stored in B-Tree form, not flat.

-> Now run same query:
SELECT * FROM orders WHERE user_id = 101;

-> What DB does:
Go to index
Binary search in tree
Jump directly to matching node
Fetch row
No full scan

-> Complexity:
Time: O(log n)

-> Real Difference (Big Impact)
Rows	    Without Index	    With Index
1,000	      Fast	          Faster
1,000,000	  Slow	          Fast
100M	      Very slow	      Still fast

-> Without Index:
Searching a name in a phonebook by reading every page

With Index:
Jump directly using alphabet section (A → B → C)

==> Tradeoff:

-> Pros
Fast SELECT queries
Efficient filtering (WHERE, JOIN, ORDER BY)


-> Cons (Why not index everything?)

1. Slower Writes
When you run:
INSERT INTO orders VALUES (1000001, 101);
DB must:
Insert row in table
ALSO update index structure (B-tree)
Extra work → slower writes

2. Extra Storage
Index is separate structure:
Table data → stored
Index data → stored separately
More disk usage

3. Over-indexing Problem
Too many indexes:
Slows down INSERT/UPDATE/DELETE
DB spends time maintaining indexes


-> When Index Helps Most
Use index on:
WHERE columns
JOIN keys
ORDER BY columns

Example:
SELECT * FROM orders WHERE user_id = 101;
Good: index on user_id


-> When Index is NOT Useful
SELECT * FROM orders;
No WHERE → index useless (still scans everything)

Composite Index (Next Level)
CREATE INDEX idx_user_status ON orders(user_id, status);

Works best for:

WHERE user_id = 101 AND status = 'paid';


-> Simple Visualization

Without Index:
[101][102][103][104][...]
   ↑ scan all

With Index:
       103
     /     \
   101     105
  /   \
100   102

→ Jump directly to 101


-> Index = extra data structure to trade storage + write speed for faster reads





==> What is a Join?
A join is used to combine rows from two or more tables based on a related column between them.
Think of it like merging Excel sheets based on a common key.

-> Example Tables

Users table:
id	name
u1	Alice
u2	Bob

Orders table:
order_id	user_id	  product
o1	      u1	      Laptop
o2	      u3	      Mouse

Notice:
u1 exists in both tables
u2 has no orders
o2 belongs to u3, who isn’t in users table


-> INNER JOIN

Definition:
Returns only the rows where there is a match in both tables.

SQL:
SELECT *
FROM orders
INNER JOIN users ON orders.user_id = users.id;

Step-by-step:
SQL checks each orders.user_id against users.id.
If it finds a match → keep the row
If no match → discard the row

Result:
order_id	user_id	  product	  id	name
o1	      u1	      Laptop	  u1	Alice

✅ Only o1 with u1 appears because only u1 exists in both tables.
❌ o2 is discarded (no matching u3 in users)
❌ u2 is discarded (no orders)

-> Key takeaway for INNER JOIN
Only “intersection” of tables
If either side doesn’t match, row is excluded


-> LEFT JOIN (or LEFT OUTER JOIN)

Definition:
Returns all rows from the LEFT table (first table) plus matching rows from the RIGHT table.
If there is no match, the right table columns are filled with NULL.

SQL:
SELECT *
FROM users
LEFT JOIN orders ON users.id = orders.user_id;

Step-by-step:
SQL keeps all rows from users.
Looks for matching orders.user_id.
If found → join the order info
If not found → fill orders columns with NULL

Result:
id	name	order_id	user_id	product
u1	Alice	o1	u1	Laptop
u2	Bob	NULL	NULL	NULL

✅ u1 has an order → shows order info
✅ u2 has no order → orders columns are NULL (still included!)

-> Visualization:

Think of LEFT JOIN as:

Users Table (LEFT)
+-----+------+
| u1  | Alice|
| u2  | Bob  |
+-----+------+

Orders Table (RIGHT)
+----------+---------+
| o1       | u1      |
| o2       | u3      |
+----------+---------+

LEFT JOIN Result:
+-----+-------+----------+
| u1  | Alice | o1       |
| u2  | Bob   | NULL     |

-> Comparison Table
Feature	          INNER JOIN	              LEFT JOIN
Rows returned	    Only matching	            All left table + matches
Missing matches	  Excluded	                Right table → NULL
Use case	        Only need exact matches	  Include all primary records, even without match

-> Example Use Case
INNER JOIN: Show users who made orders.
LEFT JOIN: Show all users, including those who never ordered → useful for reports, stats, analytics.





==> Normalization
Goal: Reduce redundancy (duplicate data) and improve data integrity.

-> Why is redundancy bad?

Example of bad design:

order_id	user_name	  user_email
1	        Rohan	      rohan@mail.com
2	        Rohan	      rohan@mail.com
3	        Priya	      priya@mail.com

-> Problem:
The same user info is repeated multiple times.
Updates are error-prone: if Rohan changes email, you need to update every row.
Wastes storage and can create inconsistencies.

-> Good Design – Normalize Tables
Split into logical tables:

Users Table

user_id	    user_name	    user_email
101	        Rohan	        rohan@mail.com
102	        Priya	        priya@mail.com

Orders Table

order_id	  user_id	  order_date
1	          101	      2026-03-24
2	          101	      2026-03-24
3	          102	      2026-03-24

-> Benefits:
Each piece of data stored once.
Easier to update info.
Saves space, avoids inconsistencies.


Normal Forms – Simplified

1NF (First Normal Form) – Remove repeating columns
Each column has atomic (single) values.
No lists or repeated groups in a column.


2NF (Second Normal Form) – Remove partial dependency
If table has a composite key, every non-key column must depend on the whole key, not just part of it.


3NF (Third Normal Form) – Remove transitive dependency
Non-key columns shouldn’t depend on other non-key columns.
Example: Don’t store user_email in orders if user_id already links to users.



--> Example (Bad Design -> 1NF -> 2NF -> 3NF):

Step 0: Bad Design (Unnormalized Table)
order_id	user_name	user_email	product_name	quantity
1	Rohan	rohan@mail.com
	Laptop	1
2	Rohan	rohan@mail.com
	Mouse	2
3	Priya	priya@mail.com
	Laptop	1

-> Problems:
user_name & user_email repeat for each order.
Updates are error-prone.
Data redundancy everywhere.


-> 1NF (First Normal Form)
Goal: Remove repeating groups / atomic values.
Each column must have a single value.
No arrays or multiple values in one column.

Example (Already Atomic):

order_id	  user_name	user_email	  product_name	  quantity
1	Rohan	    rohan@mail.com          Laptop	        1
2	Rohan	    rohan@mail.com          Mouse	          2
3	Priya	    priya@mail.com          Laptop	        1

Here, each cell is atomic. 1NF satisfied.
But still redundant data exists (user info repeated) → move to 2NF.


-> 2NF (Second Normal Form)
Goal: Remove partial dependency
If a table has a composite key, every non-key column must depend on the whole key.
Split data into logical tables.
Composite Key Example: (order_id, product_name) uniquely identifies each row.
user_name & user_email depend only on order_id, not the whole key → partial dependency.

Solution: Split Tables

Users Table:

user_id	  user_name	  user_email
101	      Rohan	      rohan@mail.com
102	      Priya	      priya@mail.com

Orders Table:

order_id	  user_id
1	          101
2	          101
3	          102

OrderDetails Table (depends on full composite key order_id + product_name):

order_id	product_name	quantity
1	        Laptop	      1
2	        Mouse	        2
3	        Laptop	      1

-> 2NF satisfied:
No partial dependencies.
Non-key columns depend on whole key.


-> 3NF (Third Normal Form)
Goal: Remove transitive dependency
A non-key column should not depend on another non-key column.
Only primary key → non-key columns dependencies allowed.

Example Issue:

If Orders table had:

order_id	user_id	  user_email
1	        101	      rohan@mail.com
2	        101	      rohan@mail.com

user_email depends on user_id → transitive dependency (order_id → user_id → user_email)

Fix: Remove transitive dependency by keeping user_email only in Users table.

-> Final 3NF Tables

Users:

user_id	  user_name	  user_email
101	      Rohan 	    rohan@mail.com
102	      Priya	      priya@mail.com

Orders:

order_id	  user_id
1	          101
2	          101
3	          102

OrderDetails

order_id	 product_name	  quantity
1	         Laptop	        1
2	         Mouse	        2
3	         Laptop	        1

==> Benefits:
No redundancy.
Easy updates (change email once in Users table).
Data integrity maintained.
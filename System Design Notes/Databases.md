For system design you need to know the difference, pros and cons between SQL and NoSQL databases: 

#### Relational (SQL - e.g., PostgreSQL, MySQL):

**Structure:** Rigid, tabular schema with rows and columns

What is it good for?
- Complex joins, relational integrity and **ACID** transactions (Atomicity, Consistency, Isolation, Durability) - making them ideal for financial data, user accounts, and inventory. 


#### Non-Relational (NoSQL): 

**Structure:** Flexible schemaless models (Key-Value, Document, Wide-Column, Graph).

NoSQL have high throughput, horizontal scalability, and handling unstructured or rapidly changing data. 

What is it good for?
- Document (MongoDB, DynamoDB): E-commerce catalogs, user profiles. 
- Key-value (Redis, Memcached): Caching, session stores, rate limiters 
- Wide-Column (Cassandra, ScyllaDB): Time-series data, high-velocity event logging.
- _Graph (Neo4j):_ Social networks, fraud detection



#### Handling Scaling Issues: 

To handle high traffic and massive data volumes, use these architectural patterns: 

###### **Replication**: Copying data across multiple nodes: 

So you have millions of users trying to READ data (looking up products on Ecommerce site) so the server starts slowing down as your DB is now trying to process thousands of read requests per second. 

To solve this you can use **Replication**. This is essentially making exact replicas of your database and put them on other servers. However there is one 'Master Server' that handles changes like user sign ups and such. But this master instantly copies these changes to its 'Slaves'. When a user wants to read data the request goes to the *slaves* not the master to distribute the traffic. 

###### Sharding: Splitting large databases into smaller, independent pieces called shards based on a sharding key

The database has grown so large it now has terabytes of data, that a single computer hard drive cant hold it anymore and searching also takes a huge amount of time. 

To solve this you split your database into smaller chunks and store each chunk in different servers. 

###### **Consistent Hashing:** A distribution technique used in distributed caches and databases (like Cassandra) to minimise data re-shuffling when nodes are added or removed.


#### Performance & Reliability Patterns: 

**Caching**: Placing an in-memory store (Redis) in front of a database to serve frequent reads instantly. 




#### Key things to note for interviews: 

So lets say you are given a scenario for the system design right. Now you have to pick if you should use PostgreSQL (AWS Aurora) or for example DynamoDB a NoSQL. Its easy to think oh you need security and ACID Compliance and GDPR so you HAVE To pick PostgreSQL. --> No. This is not the case. 

You need to consider different factors: 
- Complexity of the scenario. Do you just need a DB that has fast lookup, storing simple data like metadata etc?
- Are teams working with complex joins? Like User id's with payments, with order id's etc?
- Are access patterns consistent? Known?
- Are access patterns unknown? Constantly evolving? 
  
Access patterns is very important. For example if a Product Owner or caseworker suddenly asks for a report tomorrow joining Claims with Documents filtered by Region. you can just write a SQL query in a PostgreSQL DB -->  Without an index this would be slow. But not expensive, it would be the same base price you pay for the DB

**KEY:** Doing this in DynamoDB or NoSQL would be expensive and time consuming. You would have to scan entire tables and with dynamoDB you PAY-PER-BYTE-READ. so you are reading rows and rows trying to find status='pending' each row reading you are paying for. 

Example: 
In a relational SQL database, if you want to find all users with a specific status, you write:
```sql
SELECT * FROM users WHERE status = 'PENDING';
```

If there is no index on `status`, SQL still returns the answer, but it checks every row. 
	 index it means a literal index like at the back of a book:
	 - **WITHOUT an Index (Full Table Scan):** You have to open to Page 1 and read every single word on every page all the way to Page 1,000. It takes forever, but eventually, you find all the pages.
	 - **WITH an Index (Database Index):** You flip straight to the back of the book, look up "Catalyst" in alphabetical order, and see: `Page 42, 108, 315`. You turn directly to those exact three pages in seconds.

now lets say we have a Database with 1,000,000 users.  we run this query
```sql
-- Querying WITHOUT an index on 'status'
SELECT * FROM users WHERE status = 'PENDING';
```

The database engine has no idea where `'PENDING'` users are located. It has to perform a **Full Table Scan**: it reads row 1 from the hard drive, checks if `status == 'PENDING'`, reads row 2, checks it, reads row 3... all the way to row 1,000,000.

- **Time:** Seconds or minutes (high CPU and disk usage).

but the key point here is that with a AWS Aurora (SQL DB) you pay your flat price. Its slow but you dont pay anything crazy. with a noSQL DB, you would have to pay a crazy amount because each row will have to be read.
If your base table uses `user_id` as the primary key, but you frequently need to search by `email`, you create a GSI where `email` is the Partition Key.
- To avoid performing a full table scan when querying by an attribute that isn't the primary key, you create a **Global Secondary Index (GSI)**. A GSI acts like a **shadow table** managed automatically by AWS.
- **Cost Multiplier:** Every time an item is written or updated in the base table, AWS behind the scenes writes to the GSI as well. You pay for extra storage and write throughput for the GSI.





##### When to choose which database?
To match a database to a real-world use case, you look at whether it leans heavily toward reads or writes, and whether data accuracy or sheer speed matters more.

Example 1: E-Commerce Catalogs (Read Heavy):
- Here we would choose to use **Relational SQL (PostgreSQL)** with heavy caching OR we could use a Document Database (MongoDB)
  
  Why? if products have structured, uniform categories, SQL works well with indexes. 
  If every product has completely different attributes (e.g., a shirt has a size, but a laptop has RAM and CPU), a schemaless Document DB shines
  Both need a cache layer like Redis in front to handle millions of shoppers browsing instantly.


Example 2: News Feed (Read Heavy):
- Here we would choose NoSQL with Redis for Caching. News posts are being read by millions of users and new posts are constantly being written. 

Example 3: IoT Sensor Logs (Write Heavy):
- These primarily are for collecting data. So NoSQL DB would be good here. 
  
  why? Millions of data points are being written to the sensor log simultaneously like for temperature, speed etc. Your database needs to be able to handle high velocity high throughput and rapidly changing data.

Example 4: Financial Transactions (Write Heavy + Strict Consistency)
- Relational SQL (PostgresSQL or MySQL)
  
  Why? Data needs to follow ACID and you cant lose transacational data.

Example 5: Chat App Message Ingestion (Write-Heavy
-  Wide-Column NoSQL (Cassandra)

why? Again this is high velocity and constant. People are texting constantly and thousands of messages will be sent between users within minutes. So we would choose NoSQL here





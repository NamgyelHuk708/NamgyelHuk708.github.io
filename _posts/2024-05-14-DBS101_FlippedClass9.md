---
Title: DBS101 Flipped Class 9
categories: [DBS101, Flipped_Class9]
tags: [DBS101]
---

# Topic :  Query Optimization
----
## Materialised Views
### What is a Materialized View?
A materialized view is a duplicate data table created by combining data from multiple existing tables for faster data retrieval.

### Benefits of materialized views?
- Speed
 We can query data directly from our new view instead of having to compute new information every time.

- Data storage simplicity 
Since a material views allow us to consolidate complex query in one table, we can make comples queried more manageable as it is easy in doing data transformations and easier to maintain code.

- Consistency
As Materialized views provide a consistent view of data captured at a specific moment. We can configure read consistency in materialized views and make data accessible even in multi-user environments where concurrency control is essential.

- Improved access control
We can use a materialized view to control who has access to specific data and filter information for users without giving them access to the source tables.

## Advanced Query Optimization in DBMS
### The Importance of Query Optimization
Query optimization is vital for ensuring the performance and scalability of applications and systems that rely on databases.  Furthermore, query optimization can save computational resources and, consequently, reduce costs.

### Basic Optimization Strategies
1. Efficient Indexing: Proper use of indexes to accelerate record retrieval.
2. Reducing Returned Data: Selecting only the necessary columns and limiting results.
3. Avoiding Redundant Queries: Caching query results or preventing redundant queries.

### Advanced Query Optimization Techniques
1. Query Explainers

Query explanation tools, such as the EXPLAIN command in PostgreSQL, help understand how the database executes a query. This allows the identification of performance bottlenecks and the optimization of the execution plan.

```
// Example of using EXPLAIN in SQL
EXPLAIN SELECT * FROM products WHERE price > 100;

```
2. Index Optimization

In addition to creating indexes, it is essential to choose suitable index types, such as composite, partial, or functional indexes, to meet specific query requirements.
![alt text](<../index optimizer.webp>)
```
// Example of creating an index in PostgreSQL
CREATE INDEX idx_product_price ON products (price);

```
3. Batch Queries

Processing multiple operations in a single batch can reduce system overhead by minimizing the number of database connections and queries.

```
// Example of using batch queries in Node.js
const batchQuery = async () => {
  const queries = [
    'UPDATE products SET stock = stock - 1 WHERE id = 1;',
    'INSERT INTO records (product_id, action) VALUES (1, "Sale");',
  ];

for (const query of queries) {
    await db.query(query);
  }
};

```

4. In-Memory Storage

Using in-memory databases like Redis for queries that require low latency can significantly speed up read operations.

![alt text](../inmemeory.webp)

```
// Example of using Redis in Node.js
const redis = require('redis');
const client = redis.createClient();

client.set('key', 'value');
client.get('key', (err, reply) => {
  console.log(reply); // Output: 'value'
});

```
5. Data Denormalization
In read-intensive scenarios, data denormalization can be an effective strategy, reducing the need for complex joins.
```
// Example of denormalization in SQL
SELECT orders.id, customers.name
FROM orders
JOIN customers ON orders.customer_id = customers.id;

```
![alt text](<../data denormalization.webp>)

6. Bitmap Index Usage
Bitmap indexes are an advanced technique particularly useful in scenarios with low cardinality, where field values have a limited number of different occurrences. Instead of creating traditional indexes, bitmap indexes record which records contain specific values in fields. This is useful for queries involving filters on categorical fields, such as “status” or “type.”

![alt text](<../bitmap indexing.webp>)

```
// Example of creating a bitmap index in PostgreSQL
CREATE INDEX idx_status ON orders USING bitmap(status);

```

### What we did in the flipped class
To enhance the learing particapation of student we were divided to two main groups where we were give a different topic such as Materialised Views and Advanced Query Optimization in DBMS. After having master the topic we were set a set of MCQ for other team to see their understanding. Hence the session concluded with team 2 wining the compytation of answering.
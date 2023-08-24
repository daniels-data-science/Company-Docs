# Relational Database or Non-Relational Database

Relational databases are the best choice if your data is predictable in terms of size, structure, and access frequency. They have the capability to maintain data integrity despite errors or interruptions in data processing. On the other hand, non-relational databases work better for storing flexible or changing data, including images, videos, and documents.

## Category

**Relational database**
- Data model: Tabular
- Data integrity: High with full ACID compliance
- Performance: Improved by adding more resources to the server
- Scaling: Requires additional data management strategies
- Use cases: Applications relying on relationships between data, complex querying, and transactions

**Non-relational database**
- Data model: Key-value, document, or graph
- Data integrity: Eventual consistency model
- Performance: Improved by adding more server nodes
- Scaling: Scaling is straightforward
- Use cases: Storing semi-structured or unstructured data, real-time data, big data analytics

In general, NoSQL databases are well-suited for large amounts of semi-structured or unstructured data, real-time data, and analytics. Relational databases are suitable for data with relationships, complex querying, and transactions.

## Which Database to Use?

### PostgreSQL

Preferred for:
1. Web applications requiring reliability, analytics, and geospatial data
2. Applications needing data security and transactions
3. Applications requiring various SQL features
4. Supported Languages: .Net, C, C++, Java, Perl, Python, TC
5. Query Language: SQL

### MongoDB

Preferred for:
1. Scalable and flexible applications with unstructured data
2. Applications requiring fast performance and low latency
3. Online applications with large data stores
4. Supported Languages: Multiple languages
5. Query Language: API calls, Javascript, REST

## Conclusion

**Use MongoDB in the following scenarios:**
- Unstructured data handling
- Massive and growing data
- Cloud-based applications
- Automatic failover and replication

**Use PostgreSQL in the following scenarios:**
- Structured data with patterns
- Frequent joins
- Limited resources
- Moderate data sizes
- Transactional and ACID-compliant needs
- Large systems with critical read and write speeds
- Image storage

**Use MySQL in the following scenarios:**
- Better security
- Compatibility with various operating systems
- Client-server architecture
- Familiarity with MySQL

**The team has decided to go with MySQL database platform.**
# Introduction

In this research work, an in-depth analysis is conducted to compare and contrast different database platforms, with a focus on determining the most suitable platform for the food_remedy_API. The paper aims to provide a detailed explanation of the factors that should be considered when choosing a database platform for food_remedy_API, and the reasons why a particular platform is recommended over others.

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

After careful consideration and evaluation, the team has opted to implement the MySQL database platform for our project. One of the main reasons for this decision is the cost-effectiveness of MySQL as an open-source solution. Additionally, MySQL's ACID compliance ensures reliability, while its robust data security measures provide a strong layer of protection against potential threats. The team's familiarity and expertise using MySQL Workbench is also a key factor in our decision. With MySQL, we are confident that we have chosen a reliable and efficient database platform to support our project.
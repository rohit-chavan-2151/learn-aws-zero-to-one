## **AWS Database Services**

Amazon Web Services (AWS) offers a comprehensive suite of purpose-built, fully managed database services designed to fit specific data models and application workloads. Rather than relying on a single one-size-fits-all solution, AWS provides distinct engines for relational, key-value, document, in-memory, graph, time-series, and analytics workloads.

_Some key architectural highlights of AWS Database services are :_

- Managed Operations : AWS automates routine database administration tasks, including hardware provisioning, software patching, configuration, automated backups, and Multi-AZ failover.
- Serverless Options : Services like Aurora Serverless, DynamoDB, Keyspaces, Neptune Serverless, and Timestream scale compute and storage automatically based on demand, eliminating capacity planning.
- Generative AI & Vector Search : Multiple AWS engines—including Aurora PostgreSQL, RDS for PostgreSQL, DocumentDB, MemoryDB, and Neptune—support vector embeddings for Retrieval-Augmented Generation (RAG) and semantic search.
- Seamless Migration : The AWS Database Migration Service (DMS) helps move on-premises databases to AWS with minimal downtime, supporting both homogeneous and heterogeneous schema conversions.

---

### AWS RDS (Relational Database Service)

Amazon Relational Database Service (Amazon RDS) is a web service that makes it easier to set up, operate, and scale a relational database in the AWS Cloud. It provides cost-efficient, resizable capacity for an industry-standard relational database and manages common database administration tasks.

**Advantages of Amazon RDS** : Amazon RDS is a managed database service. It's responsible for most management tasks. By eliminating tedious manual processes, Amazon RDS frees you to focus on your application and your users. Amazon RDS provides the following principal advantages over database deployments that aren't fully managed :

- You can use database engines that you are already familiar with: IBM Db2, MariaDB, Microsoft SQL Server, MySQL, Oracle Database, and PostgreSQL.
- Amazon RDS manages backups, software patching, automatic failure detection, and recovery.
- You can turn on automated backups, or manually create your own backup snapshots. You can use these backups to restore a database. The Amazon RDS restore process works reliably and efficiently.
- You can get high availability with a primary DB instance and a synchronous secondary DB instance that you can fail over to when problems occur. You can also use read replicas to increase read scaling.
- In addition to the security in your database package, you can control access by using AWS Identity and Access Management (IAM) to define users and permissions. You can also help protect your databases by putting them in a virtual private cloud (VPC).

**Amazon RDS shared responsibility model** : Amazon RDS is responsible for hosting the software components and infrastructure of DB instances and DB clusters. You are responsible for query tuning, which is the process of adjusting SQL queries to improve performance. Query performance is highly dependent on database design, data size, data distribution, application workload, and query patterns, which can vary greatly. Monitoring and tuning are highly individualized processes that you own for your RDS databases. You can use Amazon RDS Performance Insights and other tools to identify problematic queries.

**Amazon RDS DB instances** : A DB instance is an isolated database environment in the AWS Cloud. The basic building block of Amazon RDS is the DB instance. Your DB instance can contain one or more user-created databases. The following diagram shows a virtual private cloud (VPC) that contains two Availability Zones, with each AZ containing two DB instances.

![RDSDBInstance](https://docs.aws.amazon.com/images/AmazonRDS/latest/UserGuide/images/db-instances.png)

_**Amazon RDS application architecture**_ : The following image shows a typical use case of a dynamic website that uses Amazon RDS DB instances for database storage :

![RDSApplicationArchitecture](https://docs.aws.amazon.com/images/AmazonRDS/latest/UserGuide/images/aws-cloud-deployment-architecture.png)

- The primary components of the preceding architecture are as follows :
  - Elastic Load Balancing : AWS routes user traffic through Elastic Load Balancing. A load balancer distributes workloads across multiple compute resources, such as virtual servers. In this sample use case, the Elastic Load Balancer forwards client requests to application servers.
  - Application servers : Application servers interact with RDS DB instances. An application server in AWS is typically hosted on EC2 instances, which provide scalable computing capacity. The application servers reside in public subnets with different Availability Zones (AZs) within the same Virtual Private Cloud (VPC).
  - RDS DB instances : The EC2 application servers interact with RDS DB instances. The DB instances reside in private subnets within different Availability Zones (AZs) within the same Virtual Private Cloud (VPC). Because the subnets are private, no requests from the internet are permitted.
  - The primary DB instance replicates to another DB instance, called a read replica. Both DB instances are in private subnets within the VPC, which means that internet users can't access them directly.

  > DB engines : A DB engine is the specific relational database software that runs on your DB instance. Amazon RDS supports the following database engines - IBM Db2, MariaDB, MIcrosoft SQL server, MySQL, Oracle Database, PostgresSQL

---

#### **Amazon Aurora**

Amazon Aurora is a fully managed, cloud-native relational database service built by Amazon Web Services (AWS) that is compatible with MySQL and PostgreSQL. Aurora delivers up to 6x the throughput of stock PostgreSQL and up to 6x the throughput of stock MySQL on similar hardware. Aurora is part of the managed database service Amazon Relational Database Service (Amazon RDS) which makes it easier to set up, operate, and scale a relational database in the cloud.

- _How Amazon Aurora works with Amazon RDS_ : The following points illustrate how Amazon Aurora relates to the standard MySQL and PostgreSQL engines available in Amazon RDS :
  - You choose Aurora MySQL or Aurora PostgreSQL as the DB engine option when setting up new database servers through Amazon RDS.
  - Aurora takes advantage of the familiar Amazon Relational Database Service (Amazon RDS) features for management and administration. Aurora uses the Amazon RDS AWS Management Console interface, AWS CLI commands, and API operations to handle routine database tasks such as provisioning, patching, backup, recovery, failure detection, and repair.
  - Aurora management operations typically involve entire clusters of database servers that are synchronized through replication, instead of individual database instances. The automatic clustering, replication, and storage allocation make it simple and cost-effective to set up, operate, and scale your largest MySQL and PostgreSQL deployments.
  - You can bring data from Amazon RDS for MySQL and Amazon RDS for PostgreSQL into Aurora by creating and restoring snapshots, or by setting up one-way replication. You can use push-button migration tools to convert your existing RDS for MySQL and RDS for PostgreSQL applications to Aurora.

**RDS Deployment Types** : Amazon Relational Database Service (Amazon RDS) offers three primary deployment architectures to handle availability, disaster recovery, and read scaling:

1. Single-AZ Deployment :
   - Structure : A single DB instance running in one Availability Zone (AZ).
   - High Availability / Failover : No standby or automatic failover. If the AZ or instance fails, downtime occurs until it is restored.
   - Use Case : Best for dev, test, and non-critical workloads where redundancy is not required.

2. Multi-AZ Instance Deployment :
   - Structure: A primary DB instance in one AZ paired with a synchronous passive standby replica in a different AZ.
   - High Availability / Failover : Data is replicated synchronously. In the event of a failure or planned maintenance, RDS automatically promotes the standby to primary within 1–2 minutes.
   - Use Case : Mission-critical, production workloads requiring high availability and zero data loss (RPO = 0)

3. Multi-AZ DB Cluster :
   - Structure : One writer instance and two readable standby instances distributed across three separate AZs (supported for engines like MySQL and PostgreSQL).
   - High Availability / Failover : Uses semi-synchronous replication for faster commit latencies (up to 2x faster) and automated failover in 25–75 seconds.
   - Use Case : Production workloads requiring both high availability and horizontal read scaling.

---

### **Amazon ElastiCache**

Amazon ElastiCache is a fully managed, in-memory data store and caching service provided by Amazon Web Services (AWS) that speeds up web applications by storing frequently accessed data in memory rather than querying slower disk-based databases. It helps improve application performance by storing frequently accessed data in memory.

- Stores data in RAM instead of disks for much faster read and write speeds.
- Supports Redis OSS, Valkey, and Memcached for easy integration with applications.
- Works as a fast cache layer in front of databases like Amazon RDS and DynamoDB.
- Supports clustering for high availability and better scaling.
- Provides a serverless option that automatically scales based on application traffic.

- It has two deployment models :
  - Serverless : Automatically scales capacity up and down based on application traffic with zero infrastructure management or maintenance downtime.
  - Provisioned : Gives you manual or scheduled control over node types, shard counts, and cluster mode configurations

---

### **Amazon DynamoDB**

Amazon DynamoDB is a serverless, fully managed NoSQL key-value and document database designed to deliver single-digit millisecond performance at any scale. Because AWS handles all server provisioning, patching, and hardware maintenance automatically, developers can focus purely on application logic without managing underlying infrastructure.

_**Core data model of DynamoDB**_ : The DynamoDB data model concepts include tables, items, and attributes.

- Tables : In Amazon DynamoDB, a database is a collection of tables. A table is a collection of items and each item is a collection of attributes.
  - In a relational database, a table has a predefined schema such as the table name, primary key, list of its column names and their data types. All records stored in the table must have the same set of columns.
  - In contrast, DynamoDB only requires that a table has a primary key, but does not require you to define all of the attribute names and data types in advance.
- Items and Attributes : Individual items in a DynamoDB table can have any number of attributes, although there is a limit of 400 KB on the item size. An item size is the sum of lengths of its attribute names and values (binary and UTF-8 lengths).
  - Each attribute in an item is a name-value pair. An attribute can be single-valued or multi-valued set. For example, a book item can have title and authors attributes. Each book has one title but can have many authors. The multi-valued attribute is a set; duplicate values are not allowed.
  - For example, consider storing a catalog of products in DynamoDB. You can create a table, ProductCatalog, with the Id attribute as its primary key. The primary key uniquely identifies each item, so that no two products in the table can have the same ID.
- Data Types : Amazon DynamoDB supports the following data types:
  - Scalar types – Number, String, Binary, Boolean, and Null.
  - Multi-valued types – String Set, Number Set, and Binary Set.
  - Document types – List and Map.
- Primary Key : When you create a table, in addition to the table name, you must specify the primary key of the table. The primary key uniquely identifies each item in the table, so that no two items can have the same key. DynamoDB supports the following two types of primary keys:
  - Hash Key : The primary key is made of one attribute, a hash attribute. DynamoDB builds an unordered hash index on this primary key attribute. Each item in the table is uniquely identified by its hash key value.
  - Hash and Range Key : The primary key is made of two attributes. The first attribute is the hash attribute and the second one is the range attribute. DynamoDB builds an unordered hash index on the hash primary key attribute, and a sorted range index on the range primary key attribute. Each item in the table is uniquely identified by the combination of its hash and range key values. It is possible for two items to have the same hash key value, but those two items must have different range key values.
- Secondary Indexes : When you create a table with a hash and range key, you can optionally define one or more secondary indexes on that table. A secondary index lets you query the data in the table using an alternate key, in addition to queries against the primary key. DynamoDB supports two kinds of secondary indexes: local secondary indexes and global secondary indexes. You can define up to 5 global secondary indexes and 5 local secondary indexes per table.
  - Local secondary index : An index that has the same hash key as the table, but a different range key.
  - Global secondary index : An index with a hash and range key that can be different from those on the table.
- Query and Scan : In addition to using primary keys to access items, Amazon DynamoDB also provides two APIs for searching the data: Query and Scan.
  - Query : A Query operation finds items in a table or a secondary index using only primary key attribute values. You must provide a hash key attribute name and a distinct value to search for. You can optionally provide a range key attribute name and value, and use a comparison operator to refine the search results.
  - Scan : A Scan operation reads every item in a table or a secondary index. By default, a Scan operation returns all of the data attributes for every item in the table or index. You can use the ProjectionExpression parameter so that Scan only returns some of the attributes, rather than all of them.

- Capacity Modes : You can choose how DynamoDB manages and bills for read and write throughput based on your workload patterns.

| Feature         | On-Demand Mode                               | Provisioned Mode                                                |
| --------------- | -------------------------------------------- | --------------------------------------------------------------- |
| Traffic Pattern | Unpredictable, spiky, or new workloads       | Predictable, steady, or gradual traffic                         |
| Billing         | Pay-per-request for actual reads and writes  | Pay for pre-allocated Read and Write Capacity Units (RCUs/WCUs) |
| Scaling         | Scales instantly with zero capacity planning | Scales via configured Auto Scaling rules                        |

- _**DynamoDB Global Tables**_ : Amazon DynamoDB global tables is a fully managed, multi-Region, and multi-active database feature that provides easy to use data replication and fast local read and write performance for globally scaled applications. They deliver fast local read and write performance alongside a 99.999% availability SLA for globally distributed applications.
  - Global tables automatically replicate your DynamoDB table data across AWS Regions and optionally across AWS accounts without requiring you to build and maintain your own replication solution.
  - Global tables are ideal for applications requiring business continuity and high availability through multi-Region deployment.
  - Any global table replica can serve reads and writes. Applications can achieve high resilience with a low or zero Recovery Point Objective (RPO) by shifting traffic to a different Region if application processing is interrupted in a Region.
  - Global tables are available in all Regions where DynamoDB is available.

![DynamoDBGlobalTables](https://awsfundamentals.com/assets/blog/dynamodb-global-tables/diagram-illustrating-bidirectional-synchronization-between-aws-regions-us-east-1-and-eu-west-1-using-dynamodb-global-tables-with-arrows-indicating-data-flow-and-labeled-components..gif)

- **How Global Tables Work** : A global table consists of multiple replica tables across different AWS Regions that share the same table name and primary key schema. Every replica operates in an active-active setup, meaning applications can read from and write to any Region simultaneously without custom replication code.
  - Automated Replication : When an application writes, updates, or deletes an item in one Region, DynamoDB automatically propagates those changes to all other replicas.
  - Multi-Account Support : As of 2026, you can replicate global tables across separate AWS accounts as well as Regions using resource-based policies for stronger workload isolation.
  - Settings Synchronization : Capacity modes (on-demand or provisioned), primary keys, and global secondary indexes synchronize automatically across replicas, while tags and deletion protection remain local

- **Consistency modes** : When you create a global table, you can configure its consistency mode. Global tables support two consistency modes : _multi-Region eventual consistency (MREC)_ and _multi-Region strong consistency (MRSC)_.

If you do not specify a consistency mode when creating a global table, the global table defaults to multi-Region eventual consistency (MREC). A global table cannot contain replicas configured with different consistency modes. You cannot change a global table's consistency mode after creation.

| Feature               | Multi-Region Eventual Consistency (MREC)                                         | Multi-Region Strong Consistency (MRSC)                                             |
| --------------------- | -------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------- |
| Replication Style     | Asynchronous background replication (typically under 1–2 seconds)                | Synchronous replication across Regions for zero Recovery Point Objective (RPO)     |
| Conflict Resolution   | Uses a last-writer-wins strategy based on item-level timestamps                  | Prevents conflicts by ensuring reads always return the latest committed write      |
| Topology Requirements | Supports two or more Regions within the same account or across multiple accounts | Requires three Regions (or two Regions plus a witness) within a single AWS account |
| Feature Support       | Supports Time to Live (TTL), DynamoDB Streams, and regional transactions         | Does not support TTL or transactions; Streams are optional                         |

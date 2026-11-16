## **AWS Database Services**

Amazon Web Services (AWS) offers a comprehensive suite of purpose-built, fully managed database services designed to fit specific data models and application workloads. Rather than relying on a single one-size-fits-all solution, AWS provides distinct engines for relational, key-value, document, in-memory, graph, time-series, and analytics workloads.

_Some key architectural highlights of AWS Database services are :_

- Managed Operations : AWS automates routine database administration tasks, including hardware provisioning, software patching, configuration, automated backups, and Multi-AZ failover.
- Serverless Options : Services like Aurora Serverless, DynamoDB, Keyspaces, Neptune Serverless, and Timestream scale compute and storage automatically based on demand, eliminating capacity planning.
- Generative AI & Vector Search : Multiple AWS engines—including Aurora PostgreSQL, RDS for PostgreSQL, DocumentDB, MemoryDB, and Neptune—support vector embeddings for Retrieval-Augmented Generation (RAG) and semantic search.
- Seamless Migration : The AWS Database Migration Service (DMS) helps move on-premises databases to AWS with minimal downtime, supporting both homogeneous and heterogeneous schema conversions.

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

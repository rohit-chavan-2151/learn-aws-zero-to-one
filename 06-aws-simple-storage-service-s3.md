## AWS S3 (Simple Storage Service) - Cloud Object Storage

Amazon S3 (Simple Storage Service) is a highly scalable, secure, and durable cloud-based object storage service provided by Amazon Web Services (AWS). Unlike a traditional computer file system, S3 stores files flatly as "objects" rather than in a nested hierarchy, allowing it to scale virtually infinitely to accommodate any amount of data. Customers of all sizes and industries can use Amazon S3 to store and protect any amount of data for a range of use cases, such as data lakes, websites, mobile applications, backup and restore, archive, enterprise applications, IoT devices, and big data analytics.

- S3 utilizes a flat, non-hierarchical architecture that allows the service to scale virtually infinitely. The fundamental building blocks are logical containers and the data units stored within them

**Benefits and features** :

- _Data performance and durability_ : Scale storage resources to meet fluctuating demands, with no upfront investments or resource procurement cycles. Your data is available when needed and protected against failures, errors, and threats.
- _Security, compliance, and auditing_ : Secure your data from unauthorized access using encryption and access management features. S3 also maintains compliance programs and supports numerous auditing capabilities.
- _Flexible storage options_ : Save costs without sacrificing performance. Store data across a wide range of cost-effective storage classes that support different data access levels and are designed for specific use cases.
- _Granular data control_ : Classify, manage, and report on your data using a variety of storage management features. Log activities, define alerts, and automate workflows without managing additional infrastructure.

**Common Use Cases** :

- Backups & Disaster Recovery : Storing system images, database dumps, and application logs securely.
- Data Lakes & Big Data : Holding vast amounts of raw structured or unstructured data for AI/ML processing and analytics pipelines.
- Static Website Hosting : Hosting client-side web files (HTML, CSS, JavaScript, and images) directly from a bucket without provisioning a server.
- Media Hosting : Serving high-volume images, videos, and user uploads for web and mobile applications.

#### AWS Storage Classes

- Each object in Amazon S3 has a storage class associated with it. By default, objects in S3 are stored in the S3 Standard storage class, however Amazon S3 offers a range of other storage classes for the objects that you store. You choose a class depending on your use case scenario and performance access requirements. Choosing a storage class designed for your use case lets you optimize storage costs, performance, and availability for your objects. All of these storage classes offer high durability.
- Amazon S3 offers eight distinct storage classes designed to optimize costs based on data access frequency, retrieval speed, and durability requirements. Data can be transitioned between these classes automatically using Amazon S3 Lifecycle policies.

<u>**_Storage classes for frequently accessed objects_**</u> : For performance-sensitive use cases (those that require millisecond access time) and frequently accessed data, Amazon S3 provides the following storage classes:

- **S3 Standard (STANDARD)** – The default storage class. If you don't specify the storage class when you upload an object, Amazon S3 assigns the S3 Standard storage class. It is best used for frequently accessed data, active web assets.

- **S3 Express One Zone (EXPRESS_ONEZONE)** – Amazon S3 Express One Zone is a high-performance, single-zone Amazon S3 storage class that is purpose-built to deliver consistent, single-digit millisecond data access for your most latency-sensitive applications. S3 Express One Zone is the lowest latency cloud object storage class available today, with data access speed up to 10x faster and with request costs 50 percent lower than S3 Standard. With S3 Express One Zone, your data is redundantly stored on multiple devices within a single Availability zone.

- **Reduced Redundancy Storage (REDUCED_REDUNDANCY)** – The Reduced Redundancy Storage (RRS) class is designed for noncritical, reproducible data that can be stored with less redundancy than the S3 Standard storage class.

<u>**_Storage class for automatically optimizing data with changing or unknown access patterns_**</u> : S3 Intelligent-Tiering (INTELLIGENT_TIERING) is an Amazon S3 storage class that's designed to optimize storage costs by automatically moving data to the most cost-effective access tier, without performance impact or operational overhead. S3 Intelligent-Tiering is the only cloud storage class that delivers automatic cost savings by moving data on a granular object level between access tiers when access patterns change. S3 Intelligent-Tiering is the ideal storage class when you want to optimize storage costs for data that has unknown or changing access patterns.

- For a small monthly object monitoring and automation fee, S3 Intelligent-Tiering monitors access patterns and automatically moves objects that have not been accessed to lower-cost access tiers. S3 Intelligent-Tiering delivers automatic storage cost savings in three low-latency and high-throughput access tiers.
- For data that can be accessed asynchronously, you can choose to activate automatic archiving capabilities within the S3 Intelligent-Tiering storage class. S3 Intelligent-Tiering is designed for 99.9% availability and 99.999999999% durability. S3 Intelligent-Tiering automatically stores objects in three access tiers :
  - Frequent Access – Objects that are uploaded or transitioned to S3 Intelligent-Tiering are automatically stored in the Frequent Access tier.
  - Infrequent Access – S3 Intelligent-Tiering moves objects that have not been accessed in 30 consecutive days to the Infrequent Access tier.
  - Archive Instant Access – With S3 Intelligent-Tiering, any existing objects that have not been accessed for 90 consecutive days are automatically moved to the Archive Instant Access tier.

<u>**_Storage classes for infrequently accessed objects_**</u> : The S3 Standard-IA and S3 One Zone-IA storage classes are designed for long-lived and infrequently accessed data. (IA stands for infrequent access.) S3 Standard-IA and S3 One Zone-IA objects are available for millisecond access (similar to the S3 Standard storage class). Amazon S3 charges a retrieval fee for these objects, so they are most suitable for infrequently accessed data.

- They can be used to do the following, For storing backups and For older data that is accessed infrequently, but that still requires millisecond access. For example, when you upload data, you might choose the S3 Standard storage class, and use lifecycle configuration to tell Amazon S3 to transition the objects to the S3 Standard-IA or S3 One Zone-IA class.
- These storage class differ as follows,
  - **S3 Standard-IA (STANDARD_IA)** – Amazon S3 stores the object data redundantly across multiple geographically separated Availability Zones (similar to the S3 Standard storage class). S3 Standard-IA objects are resilient to the loss of an Availability Zone. This storage class offers greater availability and resiliency than the S3 One Zone-IA class. Can be used for your primary or only copy of data that can't be re-created.
  - **S3 One Zone-IA (ONEZONE_IA)** – Amazon S3 stores the object data in only one Availability Zone, which makes it less expensive than S3 Standard-IA. However, the data is not resilient to the physical loss of the Availability Zone resulting from disasters, such as earthquakes and floods. The S3 One Zone-IA storage class is as durable as S3 Standard-IA, but it is less available and less resilient. Can be used if you can re-create the data if the Availability Zone fails, for object replicas when configuring S3 Cross-Region Replication (CRR).

<u>**_Storage classes for rarely accessed objects_**</u> : The S3 Glacier Instant Retrieval (GLACIER_IR), S3 Glacier Flexible Retrieval (GLACIER), and S3 Glacier Deep Archive (DEEP_ARCHIVE) storage classes are designed for low-cost, long-term data storage and data archiving. These storage classes require minimum storage durations and retrieval fees making them most effective for rarely accessed data.

Amazon S3 provides the following S3 Glacier storage classes:

- **S3 Glacier Instant Retrieval (GLACIER_IR)** – Use for long-term data that's rarely accessed and requires milliseconds retrieval. Data in this storage class is available for real-time access.
- **S3 Glacier Flexible Retrieval (GLACIER)** – Use for archives where portions of the data might need to be retrieved in minutes. Data in this storage class is archived, and not available for real-time access.
- **S3 Glacier Deep Archive (DEEP_ARCHIVE)** – Use for archiving data that rarely needs to be accessed. Data in this storage class is archived, and not available for real-time access.

<u>**_Storage class for Amazon S3 on Outposts_**</u> : With Amazon S3 on Outposts, you can create S3 buckets on your AWS Outposts resources and store and retrieve objects on-premises for applications that require local data access, local data processing, and data residency. You can use the same API operations and features on AWS Outposts as you do on Amazon S3, including access policies, encryption, and tagging.

| Storage Class                 | Best Use Case                                                                        | Performance & Retrieval Time                                               | Min. Duration | Data Redundancy                                           |
| ----------------------------- | ------------------------------------------------------------------------------------ | -------------------------------------------------------------------------- | ------------- | --------------------------------------------------------- |
| S3 Standard                   | Frequently accessed, high-performance data (websites, mobile apps).                  | Millisecond latency                                                        | None          | Geographically spread across ≥ 3 Availability Zones (AZs) |
| S3 Express One Zone           | High-performance, latency-sensitive applications (AI/ML training, big data).         | Single-digit millisecond latency (Up to 10x faster than Standard)          | None          | Stored in a single AZ to maximize speed                   |
| S3 Intelligent-Tiering        | Data with unpredictable or unknown access patterns.                                  | Automatically shifts data between tiers based on usage; millisecond access | None          | ≥ 3 AZs                                                   |
| S3 Standard-IA                | Data accessed less frequently but needs millisecond access when requested (backups). | Millisecond latency (with per-GB retrieval fees)                           | 30 days       | ≥ 3 AZs                                                   |
| S3 One Zone-IA                | Less critical, infrequently accessed data that can be easily recreated.              | Millisecond latency (Cheaper by ~20% than Standard-IA)                     | 30 days       | Stored in a single AZ (vulnerable to facility loss)       |
| S3 Glacier Instant Retrieval  | Long-lived archive data that is rarely accessed but requires instant delivery.       | Millisecond latency                                                        | 90 days       | ≥ 3 AZs                                                   |
| S3 Glacier Flexible Retrieval | Archived data that doesn't need immediate access (compliance logs, digital media).   | Minutes (Expedited) to hours (Standard / Bulk)                             | 90 days       | ≥ 3 AZs                                                   |
| S3 Glacier Deep Archive       | Long-term digital preservation and regulatory compliance data.                       | Lowest-cost tier; retrieved within 12 to 48 hours                          | 180 days      | ≥ 3 AZs                                                   |

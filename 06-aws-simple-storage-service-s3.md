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

### AWS Storage Classes

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

### Access management and security in S3

Amazon S3 provides features for auditing and managing access to your buckets and objects. By default, S3 buckets and the objects in them are private. You have access only to the S3 resources that you create. To grant granular resource permissions that support your specific use case or to audit the permissions of your Amazon S3 resources, you can use the following features.

- <u>**S3 Block Public Access**</u> – Block public access to S3 buckets and objects. By default, Block Public Access settings are turned on at the bucket level. The Amazon S3 Block Public Access feature provides settings for access points, buckets, accounts, and AWS Organizations to help you manage public access to Amazon S3 resources. By default, new buckets, access points, and objects don't allow public access. However, users can modify bucket policies, access point policies, or object permissions to allow public access. S3 Block Public Access settings override these policies and permissions so that you can limit public access to these resources.
  - With S3 Block Public Access, organization administrators, account administrators, and bucket owners can easily set up centralized controls to limit public access to their Amazon S3 resources that are enforced regardless of how the resources are created. You can manage Block Public Access settings at multiple levels: organization level (using AWS Organizations), account level, and bucket and access point level.
  - When Amazon S3 receives a request to access a bucket or an object, it determines whether the bucket or the bucket owner's account has a block public access setting applied. If the account is part of an AWS Organizations with Block Public Access policies, Amazon S3 also checks for organization-level settings. If the request was made through an access point, Amazon S3 also checks for block public access settings for the access point. If there is an existing block public access setting that prohibits the requested access, Amazon S3 rejects the request.
- <u>**AWS Identity and Access Management (IAM)**</u> – IAM is a web service that helps you securely control access to AWS resources, including your Amazon S3 resources. With IAM, you can centrally manage permissions that control which AWS resources users can access. You use IAM to control who is authenticated (signed in) and authorized (has permissions) to use resources.
- <u>**Bucket Policies**</u> : A bucket policy is a resource-based policy that you can use to grant access permissions to your Amazon S3 bucket and the objects in it. Only the bucket owner can associate a policy with a bucket. The permissions attached to the bucket apply to all of the objects in the bucket that are owned by the bucket owner. These permissions don't apply to objects that are owned by other AWS accounts.
  - S3 Object Ownership is an Amazon S3 bucket-level setting that you can use to control ownership of objects uploaded to your bucket and to disable or enable access control lists (ACLs). By default, Object Ownership is set to the Bucket owner enforced setting and all ACLs are disabled. The bucket owner owns all the objects in the bucket and manages access to data exclusively using policies.
  - Bucket policies use JSON-based AWS Identity and Access Management (IAM) policy language. You can use bucket policies to add or deny permissions for the objects in a bucket. Bucket policies can allow or deny requests based on the elements in the policy. These elements include the requester, S3 actions, resources, and aspects or conditions of the request (such as the IP address that's used to make the request).
- <u>**Amazon S3 access points**</u> : An Amazon S3 Access Point is a named network endpoint attached to an S3 bucket or data source that simplifies how you manage data access for multiple applications, teams, or individuals. You can configure named network endpoints with dedicated access policies to manage data access at scale for shared datasets in Amazon S3. Amazon S3 access points simplify data access for any AWS service or customer application that stores data in S3. Access points are named network endpoints that are attached to a data source such as a bucket, Amazon FSx for NetApp ONTAP volume, Amazon FSx for OpenZFS volume, or an Amazon S3 recovery point in AWS Backup.
  - You can use access points to perform S3 object operations, such as GetObject and PutObject. Each access point has distinct permissions and network controls that S3 applies for any request that is made through that access point.
  - Each endpoint enforces a customized access point policy that allow you to control use by resource, user, or other conditions. If your access point is attached to a bucket the access point policy works in conjunction with the underlying bucket policy.
  - You can configure any access point to accept requests only from a virtual private cloud (VPC) to restrict Amazon S3 data access to a private network. You can also configure custom block public access settings for each access point.

  ![accessPointsPoliciesForS3](https://miro.medium.com/v2/resize:fit:1400/1*KlacMd2c8zA6mQrM0D3qjQ.png)

- <u>**Managing access with ACLs**</u> : Access control lists (ACLs) are one of the resource-based options that you can use to manage access to your buckets and objects. You can use ACLs to grant basic read/write permissions to other AWS accounts.
  - For example, you can grant permissions only to other AWS accounts; you cannot grant permissions to users in your account. You cannot grant conditional permissions, nor can you explicitly deny permissions. ACLs are suitable for specific scenarios. For example, if a bucket owner allows other AWS accounts to upload objects, permissions to these objects can only be managed using object ACL by the AWS account that owns the object.

- <u>**S3 Object Ownership**</u> : It is an Amazon S3 bucket-level setting that you can use to both control ownership of the objects that are uploaded to your bucket and to disable or enable ACLs. By default, Object Ownership is set to the Bucket owner enforced setting, and all ACLs are disabled. When ACLs are disabled, the bucket owner owns all the objects in the bucket and manages access to them exclusively by using access-management policies.
  - Object Ownership has three settings that you can use to control ownership of objects uploaded to your bucket and to disable or enable ACLs:
  1. _ACLs disabled_ : Bucket owner enforced (default) – ACLs are disabled, and the bucket owner automatically owns and has full control over every object in the bucket. ACLs no longer affect permissions to data in the S3 bucket. The bucket uses policies to define access control.

  2. _ACLs enabled_ :
  - Bucket owner preferred – The bucket owner owns and has full control over new objects that other accounts write to the bucket with the bucket-owner-full-control canned ACL.
  - Object writer – The AWS account that uploads an object owns the object, has full control over it, and can grant other users access to it through ACLs.

- <u>**IAM Access Analyzer for S3**</u> : IAM Access Analyzer for S3 provides external access findings for your S3 general purpose buckets that are configured to allow access to anyone on the internet (public) or other AWS accounts, including AWS accounts outside of your organization. For each bucket that's shared publicly or with other AWS accounts, you receive findings into the source and level of shared access.
  - For example, IAM Access Analyzer for S3 might show that a bucket has read or write access provided through a bucket access control list (ACL), a bucket policy, a Multi-Region Access Point policy, or an access point policy. With these findings, you can take immediate and precise corrective action to restore your bucket access to what you intended.
  - The Amazon S3 console presents an External access summary in the S3 console next to your list of general purpose buckets. In the summary, you can choose the active findings for each AWS Region to see the details of the finding in the IAM Access Analyzer for S3 page. External acces findings in External access summary are automatically updated once every 24 hours.
  - When reviewing a bucket that allows public access, on the IAM Access Analyzer for S3 page, you can block all public access to the bucket with a single click.

> Difference between access point & endpoint - In AWS, Amazon S3 _Access Points_ manage who can access data inside a bucket and how they do it, while _VPC Endpoints_ manage the network path used to securely connect to AWS services without using the public internet.

| Feature       | S3 Access Point                                                                                       | VPC Endpoint (for S3)                                                                 |
| ------------- | ----------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| Primary Focus | Access Management & Identity                                                                          | Network Security & Routing                                                            |
| What it does  | Creates a unique hostname/endpoint with its own policy to simplify access for specific teams or apps. | Keeps traffic inside the AWS private network, bypassing the public internet entirely. |
| Scope         | Attached to a single S3 bucket.                                                                       | Attached to a VPC network route.                                                      |
| Best Used For | Breaking up a massive, complex bucket policy into smaller, manageable pieces for different teams.     | Securely connecting EC2 instances in a private subnet to S3.                          |

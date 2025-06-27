<h1>Storage in the Cloud</h1>

<h2>Google Cloud storage options</h2>

* Structured
* Unstructured
* Transactional
* Relational

Google's core storage products Cloud Storage, Cloud SQL, Spanner, Firestore and BigTable.

<h2>Cloud storage</h2>

Offers durable, highly available object storage. **Object storage** is a data storage architecture that manages data as objects rather than folder and file hierarchy(file storage) or chunks of a disk (block storage).

Object storage contains:
* Binary form off the actual data
* Relevant associated meta-data
* Globally unique identifier (url)

Cloud Storage
* Google's object storage product
* Can store any amount of data and retrieve it as often as needed
* Fully manageable, scalable, wide uses eg: website content, archival & disaster recovery, direct download

**Binary large object (BLOB) storage** for online content, back up & archiving, storage of immediate results.

**Buckets** Cloud Storage files are organized into *buckets* which have a globally unique name and a specific geographic location for storage to minimize latency.

**Immutable** meaning new versions are created with every change made. Administrators have the option to use versioning(overwrite or track changes) within a bucket.

**IAM roles and ACL**(Access Control Lists) support organizations security best practices. IAM roles are sufficient in most purposes. For finer control ACL using *scope* who can access and perform actions and *permissions* what actions can be performed.

**Lifecycle policies** are used to keep costs of storage own by removing objects. eg: older than, create before or recent versions

<h2>Cloud Storage: Storage classes and data transfer</h2>

**Standard Storage** is frequently accessed 'hot' data, data stored for brief periods of time.

**Nearline Storage** infrequently accessed data, once a month or less access.

**Coldline Storage** low-cost, infrequently accessed data, once every 90 days access.

**Archive Storage** lowest-cost, ideally or data archiving, online back up, disaster recovery, once a year access as it has higher costs for data access and a 365 day minimum storage duration.

All storage classes have:
* Unlimited storage (no minimum object size)
* Worldwide accessibility and locations
* Low latency and high durability
* Uniform experience - security, tools, APIs
* Geo-redundancy - load balancing traffic, geographically diverse data centers

**Autoclass** automatically transitions objects to appropriate storage classes based on the objects access patterns
* Moves data that is not accessed to colder storage classes to reduce costs
* Moves data that is accessed to Standard storage to optimize future accesses

Cloud Storage
* Pay only for what you use
* No prior provisioning of capacity
* Encrypt data on the server side
* Use HTTPS/TLS(Transport Layer Security)

Transfer of data:
* **Online Transfer** using gcloud storage command from Cloud SDK, drag and drop on Cloud Console
* **Storage Transfer Service** quick and cost effective, schedule and manage batch transfers to Cloud Storage from another cloud provider, storage region or HTTPS endpoint
* **Transfer Appliance** rackable, high- capacity storage server to leases from Google Cloud. Connect to your network, load with data, then ship it to an upload facility. Up to a petabyte of data per appliance

<h2>Cloud SQL</h2>

Fully managed relational databases including MySQL, PostgreSQL and SQL Server. Use for mundane tasks such as 
* Applying patches/updates
* Managing backups
* Configuring replications

**Cloud SQL**
* Doesn't require software installation or maintenance
* Scales up to 128 processor cores, 864 RAM and 64 TB storage
* Supports automatic replication scenarios
* Supports managed backups
* Encrypts customers data when on Google's internal networks and when stored in database tables, temporary files and backups
* Includes a network firewall

Cloud SQL is accessible by other Google CLoud services and external services. Eg drivers Connector/J for Java or MySQLdb for Python. COmpute Engines can have authorized access and can be in the same zone as CLoud SQL.

<h2>Spanner</h2>

Fully managed relational database service that scales horizontally, strongly consistent, speaks SQL.
* SQL relational database management system with joins and secondary indexes
* Built in high availability
* Strong global consistency
* High numbers of input/output operations per second

<h2>Firestore</h2>

Flexible, horizontally scalable, NoSQL cloud database for mobile, web and server development. Data is stored in documents, which has key-value pairs, and then organized into collections. Documents can contain complex nested objects in addition to subcollections.

* Retrieve individual documents
* Retrieve all the documents in a collection
* Can include multiple, chained filters
* Can combine filtering and sorting options
* Indexed by default

**Data sychronization** to updates data on any connected device. Designed to make simple one-time fetch queries efficiently even offline.

* Automatic multi-region data replication
* Strong consistency guarantees
* Atomic batch operations
* Real transaction support

<h2>Bigtable</h2>

NoSQL big data database service. Ideal for operational and analytical applications which handle massive workloads, consistent low latency, high throughput.

* More than 1 TB of semi-structured or structured data
* Data is fast with high throughput, or is rapidly changing
* NoSQL data
* Data is time-series or has natural semantic ordering
* Big data running asynchronous batch or synchronous realtime processing on the data
* machine learning algorithms on the data

Can interact with other Google CLoud services and third party clients. Using APIs, data can be read from and written to Big Table through a data service. Data can be streamed in through stream processing frameworks, or read and written through batch processes

<h2>Comparing storage options</h2>

**CLoud Storage** storing immutable blobs larger than 10 MB, capacity of petabytes, max unit size 5 TB per object

**CLoud SQL** full SQL support for an online transaction processing system, web frameworks and existing applications, up to 64 TB

**Spanner** Full SQL support for an online transaction processing system, horizontal scalability, petabytes

**Firestore** Massive scaling and predictability together with real time query results and offline query support, eg storing, syncing and querying data for mobile and web apps, terabytes, max unit size 1 MB per entity

**Bigtable** Storing large amount of structured objects, Does not support SQL queries and multi-row transactions, analytical data with heavy read and write events, eg AdTech, financial or IoT, petabytes, max unit size 10 MB p/cell, 100MB p/row

**BigQuery** the reason to store data in BigQuery is to use big data analysis and interactive querying capabilities.
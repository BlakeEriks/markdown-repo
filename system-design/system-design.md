# System Design

## Horizontal and Vertical Scaling

**Scalability** is a systems ability to handle an increased workload without sacrificing latency. There are two main ways to do this:

* **Horizontal Scaling** or scaling out, means adding more hardware to the existing pool of resources. (Adding more hosts in parallel to the existing ones)

* **Vertical Scaling** or scaling up, means adding more power to the server. It increases the power of the hardware running the system.

## Microservices

**Microservices** is an architecture style where a system uses loosely coupled services by dividing the application into a collection of separate, modular services. Microservices are more easily scaled as they are developed independently.

## Proxy Servers

A **proxy server**, or *forward server*, acts as a **channel between a user and the internet*. It separates the user from the website they're using.

They perform functions like:

* Forwarding requests
* Improve security + privacy
* Access blocked resources
* Control internet usage of employees / children
* Cache data

## CAP Theorum

Fundamental theorum within system design stating a distributed system can only provide 2 of 3 properties simultaneously:

* Consistency - every read receives the most recent write or an error
* Availability - every request receives a non-error response, regardless of it being the most recent write
* Partition Tolerance - system stays up despite messages being dropped by the network between nodes

## Redundancy and replication

**Redundancy** is the process of *duplicating critical components of a system* with the intention of increasing the reliabilty or performance. It plays a critical role in removing single points of failure.

**Replication** is the process of *sharing information to ensure consistency between redundant resources*. Software and hardware components can be replicated to improve reliability, fault-tolerance or accessibility. 

A common pattern for replication in many database management systems (DBMS) is a primary-replica relationship between the original and its copies. The primary server receives all of the updates, and those updates pass the updates to the replica servers.

## Storage

__Block Storage__ breaks data down into blocks of equal sizes and given a unique identifier to access. These blocks are stored in physical storage. Blocks can be stored anywhere in the system.

__File Storage__ is a _hierarchical storage methodology_ where data is stored in files / folders / directories. Good for limited amounts of structured data.

__Object Storage__ is designed to handle large amounts of unstructured data. It is a preferred method for archiving and backing up data as it offers _dynamic scalability_.

## Message Queues

__Message queues__ route messages from a source to destination following FIFO policy. They facilitate asyncronous behavior, allowing modules to communicate with each other without hindering any primary tasks. Message queues also facilitate cross-module communication and provide temporary storage for messages until they are processed and consumed.

__Kafka__ is a distributed system consisting of servers and clients that communicate over a TCP network protocol allowing read / write / store and process events. It is used primarily for data pipelines and streaming solutions.

## File Systems

__File systems__ are processes that manage how and where data on a storage disk is stored. It handles internal operations of the disk and provides and api for users or applications to interact with disk data.

Operations include:

* File naming
* Storage management
* Directories
* Folders
* Access rules

__Google File System (GFS)__ is a scalable, distributed file system designed for large data-intense applications. It was built to focus on batch processes on large data sets with system to system interaction, rather than user to user. It is scalable and fault-tolerant. The architecture has GFS clusters, which contain a single master and multiple chunkservers that can be accessed by multiple clients.

__Hadoop Distributed File System__ is a distributed file system that handles large sets of data and runs on commodity hardware. 

* Built for unstructured data
* Simplified form of GFS
* Built around write once, read many pattern

## Bloom Filters

Probabilistic data structure designed to answer the set membership questions -> is this element present in the set?

## Consistent Hashing

Maps data to physical nodes and ensures only a small set of keys move when servers are added or removed. Stores data managed by a distributed system in a ring, with each node in the ring assigned a range of data.

## Quorum

__Quorum__ is the minimum number of servers on which a distributed operations needs to be performed successfully before declaring the operation a success.

## Merkle trees

A __Merkle tree__ is a binary tree of hashes, where each internal node is the hash of its two children, and each leaf is a hash of the original data.

## ACID Properties

To maintain database integrity, all transactions must obey __ACID Properties__.

* __Atomicity__: A transaction is an atomic unit. All of the instructions within a transaction will succeed or none of them will.
* __Consistency__: A database is initially in a consistent state, and should remain that way after every transaction.
* __Isolation__: If multiple transactions are running concurrently, they shouldn't be affected by each other, meaning that the result should be the same as the result if they ran sequentially.
* __Durability__: Changes that have been committed to the database should remain, even following software or system failure.

## Database Indexing

__Database indexing__ makes it faster and easier to search through a table. 

- Made using 1 or more columns - basis for both rapid random lookups and efficient access of ordered info.
- While they can speed up data retrieval, they can slow insertion & updates due to their size

## Distributed Systems

A __Distributed System__ is a collection of computers that work together to form a single computer for the end user.

- All hosts share the same state
- All hosts operate concurrently
- Hosts can fail independently without affecting entire system

Benefits

- Scalability
- Modular growth
- Fault Tolerance
- Cost effective
- Low Latency
- Efficiency - breaking data into smaller pieces
- Parallelism - processors divide up complex problems into smaller chunks

Failures Include

- __System Failure__: Occurs because of failing software or hardware.
- __Communication Failure__: Occurs because of a communication link or shifting of nodes
- __Secondary Storage Failure__: Info on secondary storage device is inaccessible - result of node crashing, dirt on the medium, and parity errors
- __Method Failure__: Halts the entire system and make it unable to perform any executions

## MapReduce

Google framework made to handle large amounts of data efficiently. Uses many servers for data management and distribution. 

Workflow:

- __Partitioning__: Data starts as large chunk, and is broken into smaller pieces that are handled in parallel
- __Map__: Key-value pair structured data is passed to map workers according to user-defined map function to generate intermediate k-v pairs.
- __Intermediate Files__: The data is partitioned into R partitions (R being number of reduce workers). This is stored in memory until the primary node forwards them to reduce workers.
- __Reduce__: Reduce workers sort data and group data with same keys
- __Aggregate__: Primary node is notified when reduce workers are done. In the end, the sorted data is aggregated together and R output files are generated for the user.


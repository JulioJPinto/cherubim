
## Why are storage systems relevant?

- Cornerstone for data management infrastructures and systems:
	- Cloud, HPC, loT, ...
	- Databases, Analytics, Machine Learning, Deep Learning, ...

- Crucial to ensure data persistency and availability;

- Performance is key:
	- slow data storage and retrieval translates into slow applications and services.


## Storage Workloads

### Archival

- Data is stored for archival purposes. Useful for digital information that is rarely accessed but may be relevant in the future:
	- **Throughput** is favored over latency:
		- large amounts of data must be written/read efficiently;
		- **write-once** data typically;
		- archival files are usually append-only.
	- **Sequential** workloads:
		- archival files are written and read sequentially.
		
- Example of an archival service: _Amazon Glacier_.

### Backup

- Data backups of fresh data. Useful for digital information that is still in use and may be accessed frequently in the near future:
	- **Throughput** is still favored over latency:
		- large amount of data must be written/read efficiently.
	- **Sequential** workloads mainly:
		- sometimes one may want only to retrieve/update specific parts of backup files.
	- **Data can now be updated** typically in a sporadic fashion:
		- in some cases, **only diffs (modified data) are stored** across backups of the same data.

- Example of a backup service: _Amazon S3_.

### Primary Storage* (not only RAM!)

- Storage support for databases, data analytics, AI frameworks, VMs ...
	- **High throughput** and/or **low-latency** are now desirable:
		- large amounts of data may be written/read (throughput);
		- small sized writes/reads must be done efficiently (latency).
	- **Sequential** and **random** workloads:
		- the content of files may be partially accessed and out of order.
	- **Data** and **metadata intensive** workloads:
		- frequent access to the content of files (data) but also to different files (metadata).
	- Data is expected to be **updated frequently.**

- Example of a primary data service: _Amazon EBS_.


## Storage Mediums

- **Tape:**
	- used for archival data;
	- reliable and cheap;
	- no support for random accesses or in-place updates.

- **HDD:**
	- used for archival, backup, and (still in some cases) primary data;
	- still cheap, with support for random accesses and in-place updates.

- **SSD:**
	- used for backup and primary data;
	- more expensive than HDDs but faster, specially for random accesses.

- **Persistent Memory:**
- used for primary storage (mainly used as cache);
- speed closer to RAM for sequential and random workloads, but expensive;

- **RAM:**
	- used for primary storage (used as caches);
	- volatile, when the computer reboots data is lost...

## Storage Interfaces

- **Block Device:**
	- data is managed a set of blocks (closest abstraction to the disk);
	- e.g., Linux block device, Amazon EBS, ...

- **File System:**
	- data is managed as a hierarchy of files and directories (abstraction that most users rely on their personal computers);
	- e.g., Ext4, HDFS, Ceph, ...

- **Object Storage:**
	- data is managed as objects (e.g., each file is mapped to a key-value pair, the key is an unique file identifier, and the value is the file's content);
	- e.g., Amazon S3, Ceph, ...

## Storage Scope

### From local...

- The **Operating System (OS) mediates I/0 requests** from applications to the local disk(s);

- Applications can interact directly with the **block device layer** or ...;

- With the **file system**:
	- the **virtual file system** provides a common interface and abstraction;
	- different file system implementations must follow the VFS abstraction, while specializing it for their needs.

- The OS **page cache** holds content of files in memory for quicker access.

![[Pasted image 20241206132629.png]]

### To remote...

- **Storage** is provided **across the network:**
	- block devices;
	- file systems.

- **Client-server** architecture:
	- client I/O requests are intercepted and sent over the network;
	- at the remote machine, requests are forwarded to the server component and then stored at the local disk.

![[Pasted image 20241206132846.png]]

### To distributed... (data center)

- **Large-scale:**
	- tens of hundreds of nodes storing data;
	- Examples: HDFS, Ceph, Lustre, ...

- **No single point of failure:**
	- data distributed (replicated) across "data" nodes;
	- metadata (location of files, permissions, etc) managed by independent "meta" nodes;
	- clients contact "meta" nodes to get the location of their data. The retrieval/update of such data is done directly through the "data" nodes.

- **Manager-worker design** optimized for **stable churn** (i.e, failure of servers at a small and stable rate).

### To highly distributed... (peer-to-peer)

- **Very large-scale:**
	- thousands to millions of nodes;
	- Examples: CFS, Napster, ...

- **No single point of failure:**
	- data and metadata distributed (replicated) across several nodes (no specialized nodes);
	- clients can interact (make requests) to any node;
	- difficult to maintain a **consistent data view** across all nodes (ensuring that clients connecting to different nodes at the same time observe the same files and content).

- **Peer-to-Peer design** optimized for **high-churn** (i.e., nodes are expected to fail and rejoin the system frequently).

## Storage Features

### Data availability

- **RAID - Redundant Array of Inexpensive Driver:** data is replicated across multiple local disks in a single server for availability and load balancing purposes;

- **Replication:** data is replicated across several servers for availability and load balancing purposes;

- **Erasure-Codes:** data is broken into fragments, with redundant information, that are then spread across several servers for availability and load balancing purposes.

![[Pasted image 20241206134326.png]]

### Performance Optimizations

- **Data locality:** push computation near to the devices and/or servers holding data:
	- storage and processing co-location at the same server/device, which means faster access to data!

- **Caching:** keep data closer to the client and/or accessible from a faster source (e.g., RAM):
	- avoids waiting for data to be written/read from local or remote storagge;
	- Example: file system page cache.

### Space Efficiency

- **Compression:** removes redundant content inside and across files:
	- usually used as a static technique (i.e., for sets of files that are not going to be further updated).

- **Deduplication:** eliminates redundant copies at a storage system:
	- used as a dynamic technique (i.e., some files/blocks are expected to be updated in the future).

![[Pasted image 20241206134721.png]]

### Security

- **Data encryption:** privacy protection for sensitive data:
	- **Encryption at rest:** data is encrypted before being stored persistently;
	- **Encryption in transit:** data is encrypted at the client premises before being sent through the network.

- **Access Control:** avoid unauthorized access to users data.


## Complex and Monolithic  Storage Solutions

### Modern infrastructures

- The **I/O stack** of data centers is **long** and composed of **many components:**
	- applications, local file systems, VMs, remote storage, disks, ...
	- each providing a **strict combination of storage features**, however ...

- The best combination of features to apply varies with the applications:
	- small files versus large files;
	- storage access patterns;
	- sensitive vs non-sensitive information.

![[Pasted image 20241206135133.png]]

## Software-Defined Storage

### SDS

- Main principles:
	- I/O flows (**data plane**) are separated from the control flow (**control plane**);
	- the control plane ensures **global control of I/O flows** (logically centralized).

![[Pasted image 20241206135300.png]]

### Data Plane

- **Layered** design organized into **stages;**

- Each **stage** handles requests at the I/O path and provides different features;

- **Programmable** and **extensible** design, i.e., stages can be extended with new features.

### Control Plane

- **Global visibility** of applications, stages and infrastructure resources:
	- the brain of the system that holistically coordinates data plane stages.

- **Distributed** for scalability and availability purposes;

- Configures and tunes data plane stages to enforce I/O policies:
	- **Quality of Service:** I/O fairness or prioritization, etc.
	- **Transformations:** Encryption, compression, etc.
	- Policies are defined through **Control Applications.**
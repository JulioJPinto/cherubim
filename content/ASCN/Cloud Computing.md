# Cloud Services

Cloud Services are divided into 3 main abstractions:
- Infrastructure-as-a-Service (**IaaS**);
- Platform-as-a-Service (**PaaS**);
- Software-as-a-Service (**SaaS**).

## IaaS

- Data centers around the world;
- Each with around 80000 server;
- Top players: Google, Amazon and Microsoft.

###  Goals

- Provides virtualized hardware resources such as _computing_, _storage_ and _networking_;
- Resources allocated on **demand** and in a **pay-per-use** fashion;

## OpenStack

- Open-Source software for creating private and public clouds;
- Controls large pools of compute, storage, and networking resources throughout a datacenter;
- Managed through a dashboard or via the OpenStack API.

### Nova Service

Provides different types of compute instances:
- Baremetal Servers;
- VMs;
- Containers.

Requires integration with different other OpenStack services:
- **Keystone:** identity and authentication services;
- **Glance:** compute image repository;
- **Neutron:** provides virtual or physical networks for compute instances;
- **Placement:** tracks available hardware resources in a cloud and allocates them, for instance, when creating virtual machines.

### Cinder, Manila, and Swift services

- Compute instances have ephemeral storage provided by the OpenStack Nova service;
- For persistent storage, several services exist:
	- **Cinder:** block storage services;
	- **Manila:** file system services;
	- **Swift:** object storage services.

### Neutron and Telemetry services

- **Neutron:** delivers Networking-as-a-Service(NaaS) in virtual compute environments;
- **Telemetry:** monitoring for cloud infrastructures and virtual resources.

## PaaS

- Base on container instances;
- Supports multiple languages;
- Versioning, testing, monitoring, and logging features.

## SaaS

- Features full applications or generic software offered as a service:
	- some are software components that export their traditional APIs;
	- others are accessible as web services or through a web browser.
- **Database management systems:** there is no deployment item - the _DB_ is exposed through a client and used as a traditional _DB_ but with minimal configuration needed and with remote access;
- **SalesForce.com** and **Google Apps** like _Gmail_ are well-known instances of web-based services.

# Convenience

- **From IaaS:**
	- Avoid upfront costs on infrastructure management and hardware;
	- "Easily" deploy legacy applications.
- **To PaaS:**
	- Focus on the application development itself and its requirements;
	- Powerful development, deployment, debugging, and benchmarking tools already in place.
- **To SaaS:**
	- Leverage existing components (databases, web/application servers).


# Speed

- **From IaaS:**
	- Infrastructure is already installed and configured.
- **To PaaS:**
	- A development framework is already installed and configured.
- **To SaaS:**
	- Quick integration of different cloud software solutions.

# Elasticity

- **From IaaS:**
	- Illusion of virtually infinite resources (computation, storage, etc);
	- Users may increase/decrease computational power, storage space, ..., according to demand.
- **To PaaS:**
	- The elasticity of computational, storage, and network resources is handled by the cloud provider;
	- Usually the unit of scale is the application.
- **To SaaS:**
	- Typically the cloud software or service being provided automatically handles elasticity.


# Loss of Control

- **From IaaS:**
	- No control over hardware and virtualization software being used.
- **To PaaS:**
	- No control over specific hardware and the PaaS platform.
- **To SaaS:**
	- Third-party cloud software, which is optimized and mainly configured by the cloud provider.

# Dependability and Security

- **Dependability:** If the provider fails, the application fails and recovery is out of the control of the application owner.
- **Security:** The application is at most as secure as the provider:
	- any vulnerability of the provider is a vulnerability of the application;
	- fixes to cloud services vulnerabilities must be done by the provider.
- **Privacy:** The cloud provider holds data from users:
	- risk of data being leaked either by external or internal attacks;
	- critical data sometimes is protected by legislation that prevents some institutions from using third-party services to store such information.
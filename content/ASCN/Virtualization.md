
Technique that allows creating a software-based virtual device or resource that, in practice, is an **abstraction** provided on top of existing hardware or software resources (VMs, Virtual Networks, etc).

## Virtual Desktop Infrastructures (VDIs)

User desktop environments/terminals are provided by a central service (like VMs running on a cluster of servers).

### Basic Example of a Cloud Deployment

![[Pasted image 20241205234230.png]]

# Advantages

### Heterogeneity

- Hardware devices (physical resources) are **highly heterogeneous**:
	- different models of the same hardware type may have different interfaces, drivers, etc.
	
- Virtualization can be used to **abstract this heterogeneity** and provide unified virtual resources:
	- virtual resources present a single unified interface, independently from the underlying hardware model being virtualized.

### Transparency

- User interaction with virtual resources is similar to the interaction with a physical one (eg: when you connect through ssh to a remote machine, the interaction is identical if you are using a VM or a bare-metal server);

- **Transparency** in this context means that users do not need to change their approach when using virtual resources.

### Isolation

- Virtual resources sharing a physical resource must be **isolated**;

- **Security:** we don't want the VM of one user accessing/modifying the memory of the VMs from the other users. Such could lead to nasty attacks and memory corruption;

- **Performance:** the VM of one user should not compromise the performance of other VMs sharing the same physical resources;

- **Failures:** the failure of one VM should not lead to the failure of other VMs at the host.

### Consolidation and Management

- **Consolidation** of physical resources allows lowering costs and making better use available hardware:
	- a single server can be virtualized to run multiple operating systems (with VMs).
	
- **Managing** virtual resources is typically easier and more flexible than managing physical ones.

# Disadvantages

### Performance and Over provisioning

- Virtualization often adds a **performance** penalty to applications/servers when compared to directly using the physical resources:
	- the mechanisms used to abstract the physical hardware must perform additional tasks when mediating virtual requests into the actual hardware.
	
- Increasing the number of virtual resources being served by the same hardware may lead to **over provisioning** and performance degradation.

### Security and Dependability

- If **isolation** is not properly addressed or, a malicious user has privileged access to the physical resources, the **security** of all virtualized resources may be compromised.

- The failure of a single physical resource may compromise the **dependability** of several virtual resources using it.

# Virtual Machines

- IBM mainframe systems allowed applications to use isolated portions of a given system's resources.

- Virtualization became mainstream in the early 2000's with the X86 server architecture due to:
	- Infrastructure costs;
	- Under-utilized resources.

- Further changing an application/service to run on different Operating Systems is a costly and hard task.

Virtual Machines allow running multiple OS flavors on top of the same server. **Guest OS** instructions are intercepted, translated, and executed on the **Host's OS and hardware.**

![[Pasted image 20241206000012.png]]

## Hypervisor

- Also known as **Virtual Machine Monitor (VMM)**:
	- VMware and VirtualBox are examples of hypervisors.
	
- The hypervisor controls the low-level interaction between VMs and the underlying host's OS and hardware:
	- provides access to the host's CPU, RAM, disk and network hardware.

## Host's CPU

- **Time slicing -** processing requests are sliced up and shared across VMs;
- Similar to running multiple processes in the host OS.

## Host RAM and Persistent Storage

- Each VM allocates a specific portion of the host's RAM and persistent storage capacity;

- Memory management mostly uses traditional OS mechanisms (paging, translation lookaside buffer (TLB));

- Persistence storage is shared across VMs:
	- must handle multiple writers/readers efficiently;
	- can be allocated as required.

## Host's Network

- VMs share the host's network bandwidth and can be configured with different network setups:
	- **Host-only:** shares the host's networking namespace. The VM only has access to the host;
	- **Nat:** masks the network activity as if it is done by the host. The VM has access to external resources;
	- **Bridge:** uses the hypervisor to assign a specific IP to the VM. The VM is seen as another node in the physical network.

## Full Virtualization

- Guest OS is fully abstracted from the underlying host's hardware;

- **Advantage:** no modifications to the guest OS means higher range of supported OS flavors, and easier migration/portability of VMs;

- **Disadvantage:** all guest OS instructions must be translated by the hypervisor leading to potentially lower I/O and CPU performance:
	- hardware-assisted virtualization leverages **specific hardware** to reduce the performance penalty of instruction translation.

## Paravirtualization

- Requires hooks/modifications at the guest OS to bypass the translation of costly OS instructions;

- **Advantage:** better CPU and I/O performance as the guest OS;

- **Disadvantage:** guest OS must be modified, which is worst for maintainability and portability.


# Virtualization Types


## Type 1 - Bare Metal Hypervisor

- The hypervisor does not require a general-purpose OS at the host server:
	- the hypervisor is deployed directly on hardware as a "small operating system".

- Good performance but it usually requires specific virtualization support at the hardware level.

## Type 2 - Hosted Hypervisor

- The hypervisor is deployed on top of a general-purpose OS (VirtualBox, KVM, Xen, etc);

- Worst performance since the OS is not optimized for virtualization purposes.


# Containers

- **Lightweight virtual environment** that **groups and isolates a set of processes and resources** from the host and any other containers.

Why are they useful?

- Running different isolated versions of the same software/application in a shared OS/Kernel environment;
- Portability/migration across servers;
- Easy packaging of software, applications and their dependencies.

## Architecture

- Containers are lightweight, while **not requiring full virtualization** of CPU, RAM, network, and storage requests (as in VMs).

![[Pasted image 20241206002052.png]]

## Engine

- The **engine** isolates and configures resources:
	- containers are isolated from each other, the host is compartmentalized in terms of CPU, RAM, memory, disk, etc;
	- each container shares the hardware and kernel/OS with the host system.

## Building Blocks (components of Linux kernel)

- **Namespaces (Isolation):**
	- host resources are **partitioned** into dedicated resources that are only accessible by a certain group of processes under the same namespace;
	- allow **isolating** host resources across different containers.

- **Control Groups ( Resource Management):**
	- allow **allocating resources** among groups of processes;
	- **limit the amount of resources** per container.

- **SELinux (Security):**
	- provides **additional security** over namespaces so that a container is not able to compromise the host system and other containers;
	- enforces **access control and security policies.**

## Types of Linux Containers

- **OS Containers:**
	- containers run multiple processes and stimulate a "lightweight" operating system;

- **Application Containers (e.g., Docker):**
	- focused on deploying applications;
	- each application is seen as an independent process.

## Docker

### Docker Client

- Component used by users to interact with the Docker platform (daemon);

- Exposes the **Docker API** for:
	- running and managing containers;
	- managing networks and volumes;
	- reading logs and metrics;
	- pulling and managing images.

![[Pasted image 20241206003328.png]]

### Docker Daemon and Objects

- Docker Daemon:
	- uses the docker API for receiving requests from the Docker Client;
	- **manages Docker** images, containers, volumes, networks.

- Docker Objects:
	- **Image:** immutable file that contains the source code, libraries, and other files needed for an application to run;
	- **Container:** runnable instance of an image.

### Volumes

- Containers have an **internal file system** that is **ephemeral**, the container's data is deleted once the container is removed;

- Containers can **mount a file or directory from the host machine.** Stored data is independent from the container's internal file system and **persisted even if the container is removed:**
	- **Bind mount:** generic directory from the host. Any container or host process can access it;
	- **Volume:** special host directory managed by Docker and accessible only by containers.

### Network

- **Host:**
	- shares the host networking namespace;
	- container services are presented in the network as if run by the host;
	- ports are shared (e.g., port 80).

- **Bridge:**
	- the container is seen as another node in the physical network.

### Docker Registry

- Repository of Docker Images.

![[Pasted image 20241206004452.png]]

# Kubernetes (aka K8s)

- Automates the deployment, scaling and management of containers;

- Interesting Features:
	- network management (load balancing, service discovery, ...);
	- modular storage orchestration (NFS, Ceph, AWS, ...);
	- simplified **scheduling, self healing and scale out** for containers.

![[Pasted image 20241206115055.png]]

## Kubernetes Components

- Control Plane Components:
	- **API server:** the core component server that exposes the K8s HTTP API;
	- **etcd:** key-value store for all cluster configuration data;
	- **scheduler:** distributes unscheduled pods across the available nodes;
	- **controller-manager:** runs controllers to implement K8s API behavior.

- Node Components:
	- **Kubelet:** manages containers based on incoming Pod specification;
	- **Kube-proxy:** accepts and controls network connections to node's Pods;
	- **Container runtime:** software responsible for running containers (e.g., Docker).

## Kubernetes Cluster

- A K8s cluster is a group of a **Control Plane** and a **set of Nodes:**
	- the **Nodes** host Pods that run containerized applications;
	- the **Control Plane** manages the Nodes, Network, Storage and Pod resources in the cluster.

![[Pasted image 20241206120057.png]]

### Usage

- An **administrator** uses the **kubeadm** command-line tool to set up a cluster:
	- to initialize a cluster: _kubeadm init_;
	- to destroy a cluster: _kubeadm reset_.
	
- Clients interact with the cluster through the Control Plane using the **kubectl** command-line tool.

## Kubernetes Workloads

- A **workload** is an application running on Kubernetes:
	- whether it is a single component or several that work together, on Kubernetes you run these inside a set of **Pods**.

- A **Pod** is a group of **one or more containers** with shared storage and network resources and a specification for how to run the containers.

## Kubernetes Workloads Resources

- **Deployments** provide a declarative way to manage and scale a set of identical Pods (replicas):
	- these define a desired state for the application and manage the lifecycle of the corresponding Pods

- **ReplicaSets** ensure that a specific number of Pod replicas are running at any given time:
	- the deployment is a higher-level concept that automatically manages ReplicaSets.

![[Pasted image 20241206120644.png]]

## Kubernetes Network

- Each pod has a unique cluster-wide IP address:
	- **Networking across pods** is managed through **network overlays**(e.g., Flannel, Calico).

![[Pasted image 20241206120756.png]]

## Kubernetes Services

- A **Service** is an abstraction, built on top of the network overlay, for exposing groups of Pods over the network:
	- each Service object defines a logical set of endpoints and a policy about how to make those pods accessible;
	- different types of Service policies:
		- **ClusterIP:** exposes the Service on a cluster-internal IP;
		- **NodePort:** exposes the Service on each Node's IP at a static port;
		- **LoadBalancer:** exposes the Service externally using a external load balancer.

![[Pasted image 20241206121029.png]]

## Kubernetes Storage

- Pods can access storage volumes provided by different storage backends (AWS, NFS, GCP, ...):
	- **Ephemeral** storage - available during the pod's lifetime;
	- **Persistent** storage - available even if the pod is terminated.

![[Pasted image 20241206121249.png]]

## Kubernetes Volumes

- **PersistentVolume (PV):** a piece of storage in the cluster provisioned by an administrator or dynamically provisioned using **Storage Classes;**

- **PersistentVolumeClaim (PVC):** a user request of storage for a Pod;

- **Storage Class (SC):** provides a way for administrators to describe the types of storage they offer.

![[Pasted image 20241206121510.png]]

## Kubernetes (level up!)

- **ConfigMaps:**
	- a K8s object for storing and updating **non-confidential** Pod configurations in a key-value pair format.

- **Secrets:**
	- a K8s object to safely store **confidential** data from Pods.


## Containers vs VMs

Each technology is built with different goals and the best one depends on the targeted use case!

- VMs are useful when **full server (OS) virtualization** is needed;
- Containers are useful for managing virtual environments with heterogeneous libraries and/or applications.

- **Advantages** of Containers over VMs:
	- **Faster testing/provisioning/migration**, since containers are more lightweight;
	- **Better resource utilization and performance**, once again because they are more lightweight;
	- Can easily be **deployed** on both **physical and virtualized servers:**
		- some VM hypervisors provide nested virtualization (i.e., running a VM inside a VM).

- **Disadvantages** of Containers over VMs:
	- **Weaker isolation/security** because OS/Kernel are shared;
	- **Less flexibility in running different OSs** like Linux, Windows, etc.
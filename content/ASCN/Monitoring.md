
## Definition of Monitor

- A **monitor** observes the **activity** of a system.

![[Pasted image 20241206135817.png]]

## Monitoring Concepts

- A system contains physical and logical resources with **state:**
	- CPU, RAM, disk, virtual memory, processes, threads, ...

- **State** changes as **events:**
	- CPU/memory instructions, I/O operations, application requests...

- A **trace** is a log of events:
	- each entry at the log typically contains a **timestamp** and **other details of the event.**

- The **domain** is the set of activities (events) observed:
	- E.g., resource consumption (CPU, RAM, disk, network), I/O operations, database requests.

- The **detail** of the information being captured (monitored) varies:
	- According to the **input rate:**
		- how many events can the monitor observe per unit of time?
	- According to the **resolution:**
		- at what granularities (ms, us, ns, etc) can the monitor observe events.

- A monitor imposes **overhead**, changing the observed activity:
	- E.g., the monitor also consumes system resources (e.g., CPU, RAM, I/O), such may interfere with the system being monitored and the observations.

## Monitor Classification

- What triggers the observation/collection of events?
	- **Event-driven:** observation is triggered every time an event of interest occurs;
	- **Sampling:** observation is triggered only for a subset of events (every 100 events, ...);
	- One is **trading accuracy** (observing as many events as possible - _event-driven_) for **performance** (less overhead introduced by the monitor  - _sampling_).

- When are the observations available for users and/or systems?
	- **On-line:** collected events are sent straight away to the user and/or system (e.g., to a file or a database);
	- **Batch:** events are grouped and sent in a batch to the user and/or system;
	- One is **trading real-time observation** (on-line) for **better performance** (batch).

- How is the monitor implemented?
	- **Hardware** monitors are typically more **accurate** and have better **resolution**;
	- **Software-based** monitors are usually **less expensive**, as well as **more flexible** and **extensive** in terms of the metrics and events one can observe.

- How is the monitor designed distribution-wise?
	- **Centralized:** the monitor service is deployed on a single node (e.g., server);
	- **Distributed:** the service is spread, and even replicated, across several nodes.

- What about the scope of monitoring distribution-wise?
	- **Single node:** events collected for a single node;
	- **Distributed:** events collected for a cluster of nodes;
	- This may be orthogonal to the distributed or centralized design of the monitor service. Do not confuse the **design of the monitor** with its **distribution scope!**


## Monitor Architecture

- **Observation** of the raw events in systems (e.g., resource usage, I/O requests, ...)

- **Collection** and normalization of data (e.g., normalization of time units);

- **Analysis** of normalized data (e.g., filter, querying, summarizing);

- **Presentation** of the analysis results (e.g., dashboards, reports, alarms).

![[Pasted image 20241206154137.png]]



### Observation Layer

- Events of interest can be observed through different techniques;

- **Passive observation or spying:** no need to instrument the resources and/or applications being monitored. The monitor passively observes the system;

- **Instrumentation:** the hardware, operating system, and/or applications are instrumental to observe relevant information;

- **Probing:** the monitor interacts (probes) with the system/application being observed to collect metrics.

### Collection Layer

- Observed events can be collected and normalized through two approaches:
	- **Push-based:** events are sent by the observation layer to the collection one;
	- **Pull-based:** events are pulled by the collection layer from the observation one.

- Besides collecting data, the layer is used to **normalize** it (e.g., normalize time intervals, aggregate data, ...);

- In some cases, the layer may provide **persistency** (temporary storage) for collected events.

![[Pasted image 20241206154644.png]]

### Analysis Layer

- The analysis layer has two main goals;

- Efficient and reliable **data storage and indexing:**
	- if a comprehensive set of events is collected, the analysis component may have to persist and index large volumes of data.

- Efficient **data processing:**
	- stored and indexed data must be queryable, and sometimes analyzed in streams (e.g., for time-series analysis);

- The choice of technology for this layer depends on the type of data being analyzed and the analysis requirements (e.g., time-series database, document-oriented database, ...)

### Presentation Layer

- The presentation layer can be used for visualizing:
	- **Performance metrics** of applications and/or systems (e.g., requests throughput and latency, CPU usage, RAM consumption, ...);
	- **The configuration** of cluster resources and the applications deployed in these;
	- **Errors** at cluster resources and/or applications.

- Users can use this layer through different visual representations (e.g., dashboards, reports, ...)

![[Pasted image 20241206155245.png]]

## Elastic Stack

- **Beats:** lightweight data shippers (Observation and Collection):
	- Purpose: to observe, collect and send data to Logstash or ElasticSearch for further processing and indexing.

- **Logstash:** a data ingestion tool (Collection):
	- Purpose: to collect, transform, and send data from the various sources to ElasticSearch.

- **ElasticSearch:** a distributed, JSON-based search and analytics engine (Analysis):
	- Purpose: to index, search, and analyze data.

- **Kibana:** a data visualization and exploration tool (Presentation):
	- Purpose: to visualize and manage data from ElasticSearch.

## Monitoring and Actuation

- Monitoring can be combined with actuation to automatically apply actions as the system;

- The actions to apply are specified as **policies** (e.g., when a server’s CPU is above a given threshold migrate some VMs to another server);

- The **orchestrator** is responsible for defining the best strategy for applying policies (e.g., choose what VM(s) to migrate and to which server(s));

- The **actuator** is responsible for applying the strategy defined by the orchestrator (e.g., migrate the VM resource to another server).

![[Pasted image 20241206155844.png]]

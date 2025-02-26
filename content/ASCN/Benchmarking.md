
## Software Systems

- Software systems can assume different forms (e.g., operating system, file system, database, web server, ...);

- Systems perform useful work for users by receiving **requests**, handling these, and producing **responses;**

- Systems use physical and logical resources with limited **capacity:**
	- **Physical:** CPU, memory, disk, network, ...
	- **Logical:** locks, caches, ...

![[Pasted image 20241206165305.png]]

## System Benchmarking

### Why is it useful?

- How can one build efficient and reliable systems?
	- follow good design and implementation guidelines;
	- review and validade the code and implementation;
	- **test** (i.e., **benchmark**) implementations!

- How can one know the system is using logical and physical resources efficiently?
	- **Benchmark** the system!

- How can one know that the environment where the system is running has enough resources?
	- **Benchmark** the system in that environment.

### Ecosystem

- A benchmarking ecosystem consists of:
	- The **workload** (group of requests) being issued to the **System Under Test** (SUT);
	- The **environment** where the SUT is running;
	- The **metrics** collected to measure the performance, efficiency, and/or reliability of the SUT.

![[Pasted image 20241206165657.png]]

## Workload

- Testing systems in **production** may not be viable, or the best option:
	- imagine only knowing if your SUT works when deployed and serving users...

- One can use **traces of requests** from a real production setup instead:
	- **Advantage:** requests extracted from **real workloads;**
	- **Disadvantage:** **Hard to get (sometimes) and scale** (i.e., how can one scale a trace with 100 requests to millions of requests without losing realism?).

- Another option is to use **synthetic workloads:**
	- Use a **subset of synthetically generated requests** (e.g., set of database queries, file system operations, web requests, ...);
	- Generate parameters to **mimic different behaviors** (e.g., request type, size, parallelism):
		- following a given distribution (e.g., sequential, uniform, Poisson, ...).

## Environment

### Hardware and Software

- Knowing and setting up the right environment to run experiments is very important!
	- testing your SUT in an unrealistic environment may lead to **wrong conclusions;**
	- it is also important for others to be able to **reproduce** your results.

- One must be able to **characterize the experimental environment;**

- **Hardware:**
	- what CPU, RAM, GPU, and disk models are being used?
	- what hardware configurations are being used? (e.g., number of CPUs, amount of RAM, ...).

- **Software:**
	- what operating system is being used? And the kernel version?
	- what about the libraries and corresponding versions?
	- and finally, what are the versions of the different SUT components?

## Metrics

- The SUT will be serving **multiple user requests over time;**
- The **responses** varies:
	- some requests are served **correctly** or **incorrectly;**
	- other requests may **not be served** (i.e., the SUT rejects a request because it is too busy).

![[Pasted image 20241206171832.png]]

## Performance

### Metric: Response Time (RT)

- **RT:** The time interval between the user's request and the system's response:
	- sometimes also referred to as **latency.**

- As the **load** in the system **increases**, the **RT** of requests tends also to **increase.**

![[Pasted image 20241206172015.png]]

### Metric: Throughput

- **Throughput:** rate at which user requests are serviced by the system (i.e., operations served per unit of time);
- As the **load** in the system **increases**, the **throughput** of requests tends to increase until a certain point, reaching the system's **nominal capacity:**
	- when the system becomes **saturated**, the throughput starts decreasing.

![[Pasted image 20241206172207.png]]

## Response Time vs Throughput

- A naive view (**RT = 1 / Throughput**) is false!!!
	- this is only true when the system is busy 100% of the time executing exactly 1 request!

![[Pasted image 20241206172341.png]]

### Phases

- In the figure below, one can observe **3 distinct phases** of the system:
	- **Idle:** request are immediately handled as the system has spare capacity;
	- **Near Capacity:** requests are handled after a brief wait (throughput and RT increasing);
	- **Overload:** resources become saturated (throughput decreases while RT increases).

![[Pasted image 20241206172529.png]]

### Tradeoff

- Ideally, one would **optimize** a system to increase throughput and decrease RT but this is really hard to achieve;

- Most optimizations **trade** one metric for the other (e.g., batching requests usually improve throughput at the cost of RT).

![[Pasted image 20241206172859.png]]

## More Metrics

- **Utilization** of resources (e.g., CPU, RAM, network, disk, energy, ...);

- **Efficiency** of the system (e.g., the ratio between throughput and utilization, between throughput and energy consumption, ...);

- **Reliability** of a system (e.g., number of errors, failure, ...);

- **Availability** of a system (e.g., uptime, downtime).

## Analysis of our Metrics

- When running experiments, one must collect several **samples** for metrics of interest!
	- repeat your experiments several times to identify **abnormal behavior** (outliers);
	- remember that many workloads **may not be deterministic!**

- After collecting the samples, these must be **analyzed** and, ideally, **summarized.**

## Some Conclusions

- Use **mean**, **mode**, **median**, or **high percentiles:**
	- along with **confidence intervals (CI).**

- Combine mean and std. dev. to get the **coefficient of variation (C.O.V):
	- **Std. dev. / mean** (usually expressed as %).

- Use **visual representations** to observer and better understand your samples!
	- **Time-series** plots, **histograms**, **ECDFs**, ...

## Common Mistakes

- No goals or biased ones:
	- define the **evaluation questions** you want to answer with your experiments!

- Unsystematic approach - **Reproducibility is key!**
	- set and document your workloads, experimental environment, and configurations!

- Unrepresentative workloads and metrics:
	- choose **realistic workloads** and experiments that help answer your questions;
	- avoid being biased (i.e., don't be afraid to show the **strenghts** and **drawbacks** of the SUT).

- Wrong analysis and presentation of results:
	- **Inspect samples in time** for stability:
		- consider external phenomenons.
	- Inspect ECDFs for **distribution;**
	- Then **summarize...**
---
title: Performance Engineering 
---

# Performance Engineering

### How
- Plan and code efficient algorithms & data structures
- Profiling & evaluating (through meausurements) the execution efficiency
- understanding the organization of a computer system (architecture)

### Where
- In sequential code with ILP
    - pipelining
    - supserscalar w/ out-of-order exec
    - vector processing
- In a memory hierarchy
    - multi-level caches (+ distributed memory)
- w/ support for thread parallelism
- w/ computing processors (GPUs)


### Recomended Biography

- Computer Architecture: A quantative Approach
- The OpenMP Common Core: Making OpenMP Simple Again
- Structured Parallel Programming
- Programming Massively Parallel Processors 


## Performance Optimization and Evaluation

__Missing otimization part__

This performance evaluation can be performed at different levels

- Applications
- Programming languagues
- Compiler
- __ISA__
- Datapath Control
- Functional Units
- Transistors connections

## Badnwidth and Latency
- Bandwith or throughput
    - Total work done in a given time
    - 32k-40kx improvement for processors
    - 300-120x improvement for memory and disks

- Latency or response time
    - Time between start and completion of an event
    - 50-90x improvement of processors
    - 6-8x improvement for memory and disk

## Measuring Performance

- Typical performance metrics:
    - Response time
    - Throughput

- Speedup of X and Y

__Missing other measures__

<hr></hr>

##### Next Chapter: [Principles of Computer Design](design.md)



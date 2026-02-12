(cluster)=
# Cluster

:::{admonition} Not one big computer!
:class: note, margin
A cluster is many computers tied together.
:::

A **cluster** is a set of connected computers that work together so that they can act as a single system.
Clusters are typically used to improve performance, increase reliability, or provide a shared resource pool.

<!-- stuff below should probably be used in the Scinece Cluster section -->

## Core Concepts
- **Node** – An individual machine in the cluster (often a server or blade).  
- **Interconnect** – The network that ties nodes together ([Ethernet](https://en.wikipedia.org/wiki/Ethernet), [InfiniBand](https://en.wikipedia.org/wiki/InfiniBand), etc.).  
- **Controller / Cluster Manager** – Software that schedules jobs, monitors health, and handles communication (e.g., **[Slurm](#slurm)**, **[PBS](https://en.wikipedia.org/wiki/Portable_Batch_System)**, **[HTCondor](https://en.wikipedia.org/wiki/HTCondor)**).  
- **Scalability** – Adding more nodes should increase capacity or performance with minimal re‑engineering.  

---

## Common Types of Clusters
| Type | Goal | Use‑Case |
|------|--------------|------------------|
| **[High‑Performance Computing (HPC)](#hpc) / Supercomputing** | Maximize raw computational throughput (FLOPS) | Simulations, weather modeling, molecular dynamics |
| **Load‑Balancing / Web Farm** | Distribute incoming requests evenly | Web servers, application servers |
| **High‑Availability (HA) / Fail‑over** | Provide continuous service despite failures | Database clusters, transaction processing, critical services |
| **"Beowulf" Cluster** | Low‑cost, commodity‑hardware parallelism | Academic research, home labs |
| **Grid Computing** | Federated resources across administrative domains | Large‑scale collaborations (e.g., CERN) |
| **Storage Cluster** | Aggregate storage capacity and bandwidth | Distributed file systems (Ceph, GlusterFS, Lustre) |
| **GPU / Accelerator Cluster** | Accelerate parallel workloads with GPUs, FPGAs | Deep learning training, AI inference pipelines |

---

## Architecture & Components
1. **Head / Front‑End Node** – Entry point for users (SSH, web UI) and often runs the scheduler.  
2. **Compute Nodes** – Perform the actual work; usually headless and optimized for CPU/GPU performance.  
3. **Network Fabric** – Low‑latency, high‑bandwidth interconnect (InfiniBand, 10/25/40 GbE, RoCE).  
4. **Shared Storage** – Global file system accessible to all nodes (NFS, Lustre, CephFS, GPFS).  
5. **Management Services** – Monitoring (Ganglia, Prometheus), logging, configuration management (Ansible, Puppet).  


**Advantages**

Scalability – Add nodes to increase capacity without redesigning the whole system.

One of the biggest advantages of a cluster is scalability.
The capacity of a cluster can be increased by adding further nodes.
This process happens in a pragmatic - and sometimes automated - manner without the need of redesigning the system.

Cost‑Effectiveness – A cluster of many inexpensive nodes can out‑perform a single high‑end server at a lower cost, while its shared, standardized interface maximizes overall utilization.

In a clustered environment cost-effectiveness stems from two complementary factors.
First, by aggregating the compute power of many inexpensive, commodity nodes, a cluster can deliver a total performance that exceeds what a single, high‑end server — even at a much lower total cost.
This “many‑small‑beat‑one‑big” effect arises because the cost of a high‑performance server rises sharply with each incremental gain in CPU, memory, or accelerator capability, whereas adding another modest node incurs only a modest expense while contributing a full slice of processing power.
Second, the cluster’s shared, standardized interface—typically a common filesystem, a unified job‑scheduler, and a consistent environment across all nodes—ensures that every piece of hardware is kept busy. Jobs are queued, scheduled, and dispatched automatically, so idle time is minimized and resources are allocated where they are needed most. Together, the economies of scale from parallel hardware and the efficient, centralized management of that hardware make clusters a highly cost‑effective solution for demanding workloads.

Fault Tolerance – Failure of a single node rarely brings down the whole cluster (especially in HA configurations).

Parallelism – Enables execution of tasks that can be split across many processors (MPI, MapReduce, Spark).

Resource Pooling – Centralized storage and management simplify administration.


Disadvantages & Limitations

Complexity – Requires middleware, networking expertise, and careful configuration.

Network Bottlenecks – Performance can be limited by interconnect latency/bandwidth.

Software Compatibility – Applications must be written or adapted for parallel execution.

Power & Cooling – Larger clusters demand significant infrastructure.

Management Overhead – Monitoring, patching, and troubleshooting many nodes can be labor‑intensive.

Typical Applications

Scientific Research – Climate modeling, astrophysics, genomics.

Engineering – CFD, finite element analysis, seismic simulation.

Data Analytics – Big‑data processing with Hadoop/Spark, ETL pipelines.

Artificial Intelligence – Distributed deep‑learning training on GPU clusters.

Web Services – High‑traffic websites, micro‑service architectures.

Financial Services – Risk modeling, Monte Carlo simulations, algorithmic trading.


Examples of Notable Clusters
NameLocationApprox. Peak PerformanceNotable FeaturesSummitOak Ridge National Lab (USA)>200 PFLOPS (exascale class)GPU‑accelerated, IBM Power9 + NVIDIA V100FugakuRIKEN Center (Japan)≈442 PFLOPS (TOP500 2020)ARM‑based A64FX CPUs, high memory bandwidthTitan (retired)Oak Ridge (USA)27 PFLOPSHybrid CPU/GPU architectureGoogle Cluster (Borg)Worldwide data centersN/A (service‑level)Massive container orchestration, fault‑tolerant schedulingAmazon EC2 Cluster Compute InstancesCloud (global)Scalable on demandElastic provisioning via AWS Batch/ParallelCluster

See Also

Parallel computing – Theory and techniques for dividing work among multiple processors.
Message Passing Interface (MPI) – De‑facto standard for communication in HPC clusters.
Distributed file systems – Ceph, Lustre, GlusterFS.
Container orchestration – Kubernetes, Docker Swarm (often used on modern clusters).
Beowulf cluster – Classic low‑cost HPC design using off‑the‑shelf hardware.


This markdown is a concise synthesis of the Wikipedia article “Computer cluster” (accessed February 2026). Adjust headings, add figures, or expand sections to suit your audience or documentation style.

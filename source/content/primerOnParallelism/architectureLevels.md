{% if build == "slides" %}

## Architectural Levels of Parallelism

:::::{grid} 1 1 3 3
:gutter: 3

::::{grid-item-card} 💻 Multi-Core
**4-16 cores**  
Shared memory  
Fast communication

*Local development & testing*
::::

::::{grid-item-card} 🖥️ HPC Clusters
**100s-1000s nodes**  
Scheduled jobs  
High-speed network

*Large-scale simulations*
::::

::::{grid-item-card} ☁️ Cloud
**On-demand scaling**  
Pay-per-use  
Flexible resources

*Variable workloads*
::::

:::::

### Multi-Level Parallelism

```{mermaid}
graph TB
    O[Orchestration] --> M1[Machine 1<br/>8 cores]
    O --> M2[Machine 2<br/>8 cores]
    O --> M3[Machine N<br/>8 cores]
    M1 --> C1[Core-level]
    M2 --> C2[Core-level]
    M3 --> C3[Core-level]
```

**Strategy**: Coarse-grained between machines, fine-grained within machines

```{tip}
**Start small** → Test locally → Scale up
```

{% else %}

## Architectural Levels of Parallelism

Parallelization can occur at multiple architectural levels, each with distinct characteristics, capabilities, and use cases. Understanding these levels helps you choose the right approach for your computational needs.

### Multi-Core Architectures

**Multi-core computers** are the most accessible form of parallel hardware.
Your laptop or workstation likely has multiple cores. Todays modern personal devices typically feature 4 to 16 physical cores.

**Key Characteristics:**
- All cores share access to the same main memory (RAM)
- Communication between cores is fast and efficient
- Cores are physically close together on the same chip
- Limited by the number of cores available on a single processor

**Communication Mechanism:**
- Shared memory enables efficient data exchange
- Thread-level parallelism within a single process
- Process-level parallelism with relatively low IPC overhead

**Typical Use Cases:**
- Data processing on personal devices
- Development and testing of parallel algorithms
- Tasks that fit within the memory and computational capacity of a single machine

```{note}
**Hyper-Threading Architecture**

You may see specifications like "8 CPU / 16 threads" on modern processors. This indicates Hyper-Threading (HT), where a single physical core is optimized to handle two threads concurrently.

Important: An 8 CPU / 16 Thread machine can run **8 tasks in parallel**, not 16. However, it excels at managing two threads per core concurrently. Since threads often wait for I/O or memory operations, running two threads per core can utilize idle CPU cycles, increasing overall efficiency.
```

### Cluster Architectures (HPC)

**High-Performance Computing clusters** consist of many networked computers (nodes), each with multiple cores. Academic institutions often provide access to such systems for research computing.

**Key Characteristics:**
- Hundreds to thousands of individual multi-core nodes
- Nodes connected via high-speed network infrastructure
- Shared or distributed file systems for data access
- Managed by workload schedulers (e.g., [Slurm](https://en.wikipedia.org/wiki/Slurm_Workload_Manager), PBS)

**Communication Mechanism:**
- Jobs scheduled across nodes by resource manager
- Network-based communication between nodes (higher latency than multi-core)
- Each node can use multi-core parallelism internally
- Multi-level parallelism: parallel jobs across nodes, each using multiple cores

**Typical Use Cases:**
- Large-scale scientific simulations
- Parameter sweeps requiring hundreds or thousands of runs
- Problems requiring more memory or compute than available on single machines
- Batch processing of many independent tasks

**Advantages:**
- Massive computational capacity
- Well-suited for embarrassingly parallel problems
- Optimized infrastructure and support for research computing

**Challenges:**
- Job scheduling queues may introduce wait times
- Network communication between nodes adds overhead
- Requires learning cluster-specific tools and submission systems

### Cloud Architectures

**Cloud computing platforms** (AWS, Google Cloud, Azure, or institutional clouds) provide on-demand access to computational resources that can be dynamically scaled.

**Key Characteristics:**
- Flexible resource allocation (scale up or down as needed)
- Pay-per-use model or institutional allocations
- Access to specialized hardware (GPUs, high-memory instances)
- Infrastructure-as-code for reproducible setups

**Communication Mechanism:**
- Similar to clusters: network-based communication between instances
- Can provision multiple instances, each with multiple cores
- Orchestration typically managed by cloud-native tools or custom scripts
- Storage often separate from compute (object storage, network file systems)

**Typical Use Cases:**
- Variable workloads that don't require constant resources
- Projects requiring specialized or diverse hardware configurations
- Collaborative work requiring shared remote infrastructure
- Integration with cloud-native data processing services

**Advantages:**
- On-demand scaling without waiting in queues
- Access to latest hardware without local investment
- Geographic distribution and redundancy options
- Integration with managed services (databases, machine learning platforms)

**Challenges:**
- Cost management requires careful monitoring
- Network latency can impact tightly coupled workloads
- Different mental model compared to traditional HPC
- Responsibility for infrastructure setup and security

### Multi-Level Parallelism

In practice, cluster and cloud architectures consist of many networked multi-core computers. This means **parallelization can occur simultaneously at multiple levels**:

1. **Between machines**: Distributing independent jobs across multiple nodes or cloud instances
2. **Within machines**: Each node/instance uses multi-core parallelism for its assigned task

```{mermaid}
graph TB
    O[Orchestration Layer] --> M1[Machine 1<br/>8 cores]
    O --> M2[Machine 2<br/>8 cores]
    O --> M3[Machine N<br/>8 cores]
    M1 --> C1[Core-level<br/>parallelism]
    M2 --> C2[Core-level<br/>parallelism]
    M3 --> C3[Core-level<br/>parallelism]
```

This hierarchical structure offers flexibility but requires careful planning:
- Use coarse-grained parallelism between machines (minimize network communication)
- Use fine-grained parallelism within each machine (leverage shared memory)
- Avoid over-subscription: don't request more threads than available physical cores

### Choosing the Right Level

The appropriate architectural level depends on your problem characteristics:

| Problem Characteristic | Recommended Level |
|------------------------|-------------------|
| Fits on laptop, moderate computation | Multi-core (local) |
| Embarrassingly parallel, many runs | Cluster or Cloud |
| Large memory requirements (> 64 GB) | HPC nodes or high-memory cloud instances |
| Tightly coupled, frequent communication | Multi-core or single high-performance node |
| Variable resource needs | Cloud |
| Sustained computational campaigns | HPC cluster |
| GPU acceleration required | Cloud or specialized HPC nodes |

```{tip}
**Start small**: Develop and test your parallelization approach on your local multi-core machine before scaling to clusters or cloud. This iterative approach helps identify issues early and reduces wasted resources.
```

{% endif %}

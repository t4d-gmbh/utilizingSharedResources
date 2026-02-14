{% if build == "slides" %}

## Conceptual Framework

:::::{grid} 1 1 2 2
:gutter: 3

::::{grid-item-card} Concurrency vs. Parallelism
**Concurrency**: Switching between tasks  
**Parallelism**: Simultaneous execution

*Limited by physical cores*
::::

::::{grid-item-card} Processes vs. Threads
**Processes**: Isolated, own memory  
**Threads**: Shared memory, faster

*Choose based on isolation needs*
::::

:::::

### The Parallel Workflow

```{mermaid}
graph LR
    A[Orchestration] --> B1[Job 1]
    A --> B2[Job 2]
    A --> B3[Job 3]
    B1 --> C[Aggregation]
    B2 --> C
    B3 --> C
```

**Key**: Match problem coupling to architecture
- **Embarrassingly parallel** → Easy to scale
- **Tightly coupled** → Communication overhead

{% else %}

## Concurrent vs. Parallel

Think of eating cake while singing: you can do them *concurrently* (alternating bites and verses) but not *in parallel* (simultaneously).

- **Concurrency**: Multiple tasks making progress by switching between them
- **Parallelism**: Multiple tasks executing truly simultaneously

True parallelism often needs multiple physical cores—one per task. This hardware constraint is why we can't just "make everything parallel."

## Processes vs. Threads

**Processes**: Independent program instances, each with their own memory space. They are isolated from one another and require explicit mechanisms for communication (Inter-Process Communication, or IPC).

**Threads**: Lightweight units sharing memory within a process. Fast communication but risk race conditions.

Which to use?
- Need isolation → processes
- Need fast communication → threads  
- Language constraints matter (Python's Global Interpreter Lock limits threads)

## The Typical Parallel Workflow

Three stages:

1. **Orchestration**: Initial setup and task distribution across available resources
2. **Individual Jobs**: Independent or semi-independent computation on distributed resources
3. **Aggregation**: Collection and synthesis of results from all tasks

```{mermaid}
graph LR
    A[Orchestration] --> B1[Job 1]
    A --> B2[Job 2]
    A --> B3[Job 3]
    A --> B4[Job N]
    B1 --> C[Aggregation]
    B2 --> C
    B3 --> C
```

This pattern is remarkably universal, appearing in contexts ranging from multi-core laptop computations to large-scale distributed systems. Understanding this workflow helps identify where parallelization can be applied and what communication overhead to expect.

### Information Exchange Requirements

The efficiency of a parallel solution depends heavily on how frequently tasks must exchange information:

- **Embarrassingly Parallel**: Tasks require little to no information exchange after orchestration. These problems are ideal for parallelization and easiest to implement efficiently.

- **Loosely Coupled**: Tasks need occasional information exchange (a few times per second or less). Communication overhead is manageable with proper architecture.

- **Tightly Coupled** (Fine-grained parallelism): Tasks must exchange information frequently (many times per second). These scenarios are challenging to parallelize efficiently due to communication costs and synchronization overhead.

As a general principle: **Start by determining if your problem is embarrassingly parallel**. If it is, parallelization is almost always worthwhile. For tightly coupled problems, carefully evaluate whether the communication overhead will negate the benefits of parallel execution.

### Information Flow in the Workflow

Different stages of the parallelization workflow have different communication characteristics:

- **During Orchestration**: Nearly all parallel workflows require information dissemination to initialize tasks with appropriate parameters, data subsets, or configuration
  
- **During Execution**: Requirements vary greatly depending on problem coupling:
  - Embarrassingly parallel jobs may need zero communication
  - Tightly coupled jobs require continuous information exchange
  
- **During Aggregation**: Most workflows require collecting results from all tasks, though the volume can range from simple success/failure signals to large datasets

Understanding these communication patterns helps in selecting appropriate hardware architectures and software frameworks for your specific use case.

{% endif %}

### Concurrency Workflow

::::{grid}
:gutter: 2

:::{grid-item}
:columns: 7
:class: sd-m-auto

```{image} ./../_static/concurrencyOrchestration.png
:alt: Orchestration
:width: 100%

```

:::
:::{grid-item}
:columns: 5
:class: sd-m-auto

{% if slide %}

* **Concurrency**: Multiple tasks progressing over a period of time.
* **Parallelism**: Multiple tasks executing truly simultaneously.

**Challenge**:

* Concurrency requires a strict orchestration ruling out indeterminacy.
* Parallelism adds complexity by combining multiple processing "lanes".

{% else %}

Concurrency can conceptually be broken up into 4 interacting parts:

**Orchestration**: The overarching structure and schedule of tasks are determined. Dependencies are mapped, and necessary resources are identified before execution begins.  

{% endif %}
:::
::::

{% if page %}

**Initiation**: The individual execution units (processes, threads, or coroutines) are spawned. Required data and specific execution parameters are distributed to these units.  
**Job(s)**: The discrete, independent units of work are executed. This encompasses the actual computational processing or I/O operations performed by the allocated resources.  
**Aggregation**: The outputs from the completed jobs are collected, synchronized, and consolidated. Execution is typically halted until all concurrent units have successfully reported their final state or results.  

This pattern is remarkably universal, appearing in contexts ranging from multi-core laptop computations to large-scale distributed systems.
Understanding this workflow helps identify where concurrency frameworks can be applied and what communication overhead to expect.

Parallelism requires multiple physical cores — one per task executing simultaneously.
This hardware constraint limits the universal application of parallel execution.
However, modern software applications frequently perform I/O operations, await external input, execute network requests, or offload workloads to dedicated accelerators (e.g., GPUs).
In such situations, the software thread does not need to occupy the CPU and can be paused (or blocked), freeing up CPU capacity until those auxiliary activities complete.
This is where **concurrency becomes valuable even on a single core**: while one thread is blocked by I/O, CPU cycles can be reallocated to another thread to maintain progress.
While this does not constitute true parallelism, overall throughput and responsiveness are improved by preventing CPU idling during slow operations.

{% endif %}

## Parallelism

::::{grid} 1 1 2 2
:gutter: 2

:::{grid-item}
:class: sd-m-auto

```{compound}
{.centered}
An analogy: eating and singing can be performed *concurrently* (alternating actions) but not *in parallel* (simultaneously).

```

:::

:::{grid-item-card} Concurrency & Parallelism
:class: sd-m-auto

**Concurrency**: Progress multiple tasks over a period of time.

**Parallelism**: Simultaneous execution of multiple tasks.

*Parallelism is a form of concurrency that is limited by the number of physical cores.*
:::
::::

{% if page %}

The efficiency of a parallel solution depends heavily on how frequently tasks must exchange information:

* **Embarrassingly Parallel**: Tasks require little to no information exchange after orchestration. These problems are ideal for parallelization and are the easiest to implement efficiently.
* **Loosely Coupled**: Tasks need occasional information exchange (e.g., a few times per second or less). Communication overhead is manageable with proper architecture.
* **Tightly Coupled** (Fine-grained parallelism): Tasks must exchange information frequently (e.g., many times per second). These scenarios are challenging to parallelize efficiently due to communication costs and synchronization overhead.

As a general principle: **Problem evaluation should begin by determining if the workload is embarrassingly parallel**. If so, parallelization is generally advantageous. For tightly coupled problems, the communication overhead must be carefully evaluated to ensure it does not negate the benefits of parallel execution.

### Information Flow in the Workflow

Different stages of the parallelization workflow possess different communication characteristics:

* **During Initiation**: Nearly all parallel workflows require information dissemination to initialize tasks with appropriate parameters, data subsets, or configurations.
* **During Execution**: Requirements vary greatly depending on problem coupling:
  * Embarrassingly parallel jobs may require zero communication.
  * Tightly coupled jobs require continuous information exchange.
* **During Aggregation**: Most workflows require collecting results from all tasks, though the volume can range from simple success/failure signals to large datasets.

Understanding these communication patterns aids in the selection of appropriate hardware architectures and software frameworks for specific use cases.

{% endif %}

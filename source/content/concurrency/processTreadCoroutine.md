## Processes vs. Threads vs. Coroutines

{% if slide %}

:::::{grid}
:gutter: 2

::::{grid-item-card} Processes vs. Threads vs Coroutines
:class: sd-m-auto

**Processes**: Isolated, own memory, consists of one or many threads.  
**Threads**: Minimal, manageable sequence of instructions.  
**Coroutines**: Suspendable tasks executed by threads via cooperative multitasking.

*Multi-threading allows to use idle-time of one thread for other operations*
::::
::::{grid-item}
:class: sd-m-auto

:::{admonition} Analogy
:class: tip

**The Process (The Workshop Facility)**
Isolated facility provisioned by the operating system. Memory space is encapsulated and strictly bounded.

**The Threads (The Workers)**
Execution engines deployed within the facility. Shared access to identical resources is granted.

**The Physical Cores (The Workstations)**
Hardware allocated by the central scheduler. Worker affinity can be strictly bound for execution reproducibility.

**The Coroutines (The Suspendable Projects)**
Discrete projects managed via cooperative multitasking. Execution is suspended during I/O latency to allow reallocation of worker effort.

:::
::::
:::::

{% else %}

**Processes**: Independent program instances, each with their own memory space. They are isolated from one another and require explicit mechanisms for communication (Inter-Process Communication, or IPC).

**Threads**: Lightweight units sharing memory within a process. Fast communication but risk race conditions.

**Coroutines**: Can be understood as suspendable tasks that are processed by a thread.

:::{admonition} Analogy
:class: tip

**The Process (The Workshop Facility)**
An isolated workshop facility is provisioned by a central municipality (the operating system). This facility encapsulates a shared pool of tools and raw materials (process memory space). Strict physical boundaries are enforced to prevent interference from external facilities, ensuring memory isolation.

**The Threads (The Workers)**
Within this isolated facility, one or multiple workers (threads) are deployed as the primary execution engines. All workers operating inside the facility are granted concurrent access to the identical shared pool of resources.

**The Physical Cores (The Workstations)**
Physical workstations (hardware CPU cores) are allocated to the facility by the municipality's centralized scheduler.
If multiple workstations are provisioned and multiple workers are deployed, true parallel execution is achieved.
To guarantee execution reproducibility and minimize timing variance, specific workers can be rigidly bound to specific workstations (analogous to strict thread affinity configurations in standard open-source kernels).

**The Coroutines (The Suspendable Projects)**
A queue of discrete, independent projects (coroutines) is maintained within the facility.
Cooperative multitasking is utilized by the workers to maximize continuous utilization.
When a specific project is blocked by an external dependency—such as a mandated waiting period for material delivery (I/O latency)—progress is voluntarily suspended.
The exact state of the project is preserved on the workbench.
The worker's effort is immediately reallocated to advance an alternative project from the queue.
Upon resolution of the external dependency, the preserved project is subsequently resumed by an available worker from the precise point of suspension.
:::

{% endif %}


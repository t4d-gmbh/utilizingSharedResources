(hpc)=
## High Performance Computing (HPC)


{% if slide %}
:::::{grid} 2
::::{grid-item-card} <i class="fas fa-server"></i> The Concept
- **Cluster**: Aggregation of individual computers
- **Interconnected**: High-speed (internal) networking
- **Access**: Streamlined interface
::::

::::{grid-item-card} <i class="fas fa-rocket"></i> The Goal
- **Scalability**: Tackle larger workloads
- **Performance**: Solve problems faster
- **Efficiency**: Optimize hardware utilization
- **Equitable Access**: Ensure balanced resource sharing
::::
:::::
{% else %}

HPC aggregates the processing power of many individual computers, servers, or specialized nodes into a coordinated system that delivers performance far beyond single workstation capabilities.
By employing parallel architectures, high‑speed interconnects, and optimized software stacks, HPC enables the execution of large‑scale simulations, data‑intensive analyses, and other computationally demanding workloads.

{% endif %}

<!-- Rest might go to science cluster intro -->


{% if page %}
Understanding the physical separation of roles in a cluster is critical for effective usage.

### Login Node
:::{admonition} Redundancy
:class: note, margin
Multiple login nodes for fault-tolerance and load-balancing are common.
In this case they share a filesystem (usually on a network‑attached storage).
:::

The login node(s) are the only machines users connect to directly via SSH.
They act as the “doorway” to the rest of the cluster.

Typical activities:
- ✅ **Do** edit scripts, compile code, manage files, and submit jobs (e.g., `sbatch`, `srun`).
- ❌ **Do not** run long‑running or resource‑intensive calculations here.
  Heavy workloads belong on compute nodes; crashing a login node can block access for all users.

### Controller

The Controller, aka _scheduler_ or _workload manager_, acts as a broker distributing the users requests onto the compute nodes.
Usually, the controller is a dedicated machine (or machines) but the controller can run on a login node

Typically, users submit a "job script" to a scheduler software (commonly [Slurm](#slurm) or PBS)

You cannot log into compute nodes directly.
The controller acts as a broker:
1.  You ask for resources (e.g., "I need 40 CPUs for 2 hours").
2.  The controller queues your request.
3.  When resources are free, it allocates specific nodes to you and runs your script.

#### Compute Nodes
These are the "muscle" of the system. They are often stripped-down machines (headless) optimized purely for number crunching. They access your files via a shared network filesystem.
{% endif %}

<!-- goes to principles in shared resources -->

{% if build == "slides" %}
---
{% else %}
## The "Shared" Reality
{% endif %}

{% if slide %}
:::::{grid} 2
::::{grid-item}
<i class="fas fa-users"></i> **Multi-Tenant**
- You are not alone!
- Resources are finite.
- "Idle" jobs block others.
- Unused or paused VM's deprive resources.
::::

::::{grid-item}
<i class="fas fa-balance-scale"></i> **Fair Share (Cluster)**
- Priority is dynamic.
- Heavy users get lower priority over time.
- Accurate time estimates = happier scheduler.
::::
:::::
{% endif %}

:::{admonition} Walltime
:class: tip
The **Walltime** is the maximum real-world time your job is allowed to run.
If your job hits this limit, the scheduler kills it immediately.
Always overestimate slightly (e.g., +20%).
:::

{% if page %}
Moving from a personal laptop to an HPC cluster requires a shift in mindset regarding resource usage.

### Fair Share Policy
HPC resources are expensive and shared among hundreds of researchers.
Schedulers use a "Fair Share" algorithm to determine job priority.


### Resource Request Accuracy
When submitting jobs, you must specify the **Walltime** (duration) and **Memory**.
* **Requesting too much:** Your job will sit in the queue longer because it's harder for the scheduler to find a large "hole" in the schedule for you.
* **Requesting too little:** Your job will be killed by the system (OOM - Out of Memory) before it finishes.

Profiling your code on a small scale is the best way to estimate these requirements accurately.
{% endif %}

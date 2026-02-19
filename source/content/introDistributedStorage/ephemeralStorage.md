(EphemeralStorage)=
### Ephemeral Storage

:::{admonition} The "Scratchpad"
:class: tip, margin
{% if slide %}
Fast and quickly gone.
{% else %}
High-speed workspace for heavy I/O, but wiped clean when the work is done.
{% endif %}
:::
{% if slide %}

```{compound}
{.centered}
Lightning-fast temporary storage for active workloads.

```

{% else %}

A specialized storage tier exists to meet the unique demands of high-performance computing: Ephemeral Storage.
This tier is engineered purely for speed and throughput, at the expense of long-term persistence and redundancy to feed data to CPUs and GPUs as fast as possible.

In practice, Ephemeral Storage comes in two distinct flavors:

**Global Scratch**:

In large clusters where a job may span hundreds of nodes, standard persistent shard filesystems are often too slow to handle the aggregate I/O demand.
The solution is an Ephemeral Shared Filesystem (utilizing technologies like Lustre, GPFS, or a flash-optimized CephFS pool).

This tier allows hundreds of nodes to read and write to the same dataset simultaneously.
However, because high-performance storage is a limited resource, it is usually governed by strict "Purge Policies".
Data stored here — often in directories like `/scratch/<user>` — is automatically deleted after a set period (e.g., 30 days).
It serves as scratchpad for heavy calculations, but never as a permanent storage for results.

**Local Scratch**:

In both Cloud (OpenStack) and HPC (Slurm), access to local Ephemeral Storage might also be possible.
This is the physical SSD or NVMe drive directly inside the compute node a job is running on, or a physical disk on a host machine in a cloud.

Unlike Global Scratch, this storage is isolated and not actually shared at all.
Local Scratch often provides the absolute lowest latency because there is no network overhead.
It is ideal for temporary files, spillover when RAM is full (swap), or unzipping datasets for a specific job.
However, Local Scratch is strictly volatile: the moment job finishes or a VM is terminated, this data is instantly wiped.

#### Architecture

{% endif %}

::::{grid}
:gutter: 2

{% if page %}
:::{grid-item}
:columns: 6
:class: sd-m-auto

Local Ephemeral physically resides inside the compute node's chassis (Direct Attached Storage), operating independently of the broader network. Global Ephemeral, on the other hand, utilizes a parallel shared filesystem backend connected via high-throughput network switches, stripping files across dozens of NVMe storage servers to maximize aggregate bandwidth for the entire cluster.

{% endif %}

:::
:::{grid-item}
:columns: {% if page %}6{% else %}12{% endif %}
:class: sd-m-auto

```{image} ./../_static/ephemeralStorage.png
:alt: ephemeralStorage
:width: 100%

```

:::
::::

#### Usage

{% if slide %}
{.smaller}

* Request local storage via scheduler (e.g., Slurm: `--tmp=100G`).
* Point application cache to `$TMPDIR`.
* Stage large shared datasets to `/scratch/`.
* **Move results to permanent storage before they are purged!**
{% else %}

Interacting with Ephemeral Storage depends entirely on whether you are using the Local or Global variant.

For **Global Scratch**, access feels identical to a standard shared network drive. The path is typically a well-known mount point, such as `/scratch/` or `/lustre/scratch`. Users manually copy (stage) their heavy datasets to this location before executing a distributed job. The critical operational rule here is memory: users *must* script their workflows to copy the final output data back to persistent storage (like S3 or their Home Directory) before the automated purge scripts permanently delete it.

For **Local Scratch**, the workflow is highly dynamic and usually managed by the workload scheduler (like Slurm). When a compute job starts, the scheduler creates a private, temporary folder on the node's physical NVMe drive. It exposes this path to your script via an environment variable—most commonly `$TMPDIR`. Applications and scripts should be configured to write their temporary files, cache, or RAM-spillover to this variable. The exact millisecond the job completes or fails, the scheduler forcefully runs `rm -rf` on that directory, isolating your data from the next user.

{% endif %}

#### Use Cases

{% if slide %}
::::{grid}
:gutter: 1

:::{grid-item-card} Intermediate Processing
:class: sd-shadow-s
:columns: 4
:::
:::{grid-item-card} Distributed Checkpoints
:class: sd-shadow-s
:columns: 4
:::
:::{grid-item-card} Heavy Random I/O
:class: sd-shadow-s
:columns: 4
:::

::::

{% else %}

**Intermediate Processing (Local)**:  
Unzipping a massive dataset, preprocessing the raw text or images on a single node, and deleting the raw files immediately to completely bypass network bottlenecks.

**Distributed Checkpoints (Global)**:  
Saving the state of a massive Deep Learning model every epoch across 50 active nodes. If the job crashes, it can be instantly restarted from the shared global checkpoint without losing days of progress.

**Heavy Random I/O (Local/Global)**:  
Workloads that execute thousands of tiny reads/writes per second (such as SQLite databases or massive pandas dataframe manipulations) which would choke the metadata servers of standard persistent storage.

#### Pros & Cons

{% endif %}

| Pros | Cons |
| --- | --- |
| **Maximum Performance**{% if page %}:<br>Provides the lowest latency (Local) and massive aggregate bandwidth (Global).{% endif %} | **High Volatility**{% if page %}:<br>Data is permanently destroyed upon node failure, job completion, or when the automated purge policy triggers.{% endif %} |
| **System Stability**{% if page %}:<br>Offloading heavy I/O activity to Ephemeral tiers keeps the Persistent storage tiers responsive and stable.{% endif %} | **Isolation vs. Contention**{% if page %}:<br>Local scratch isolates data completely; Global scratch is susceptible to "noisy neighbors" clogging the network bandwidth.{% endif %} |

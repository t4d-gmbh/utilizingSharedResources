## HPC Cluster Features

{% if page %}

Modern High Performance Computing (HPC) Workload Managers, like Slurm, perform much more than the simple execution of scripts.
It serves as the orchestration engine for a cluster infrastructure.
It manages large pools of compute nodes, GPUs, and parallel storage systems throughout a datacenter, turning them into a single programmable entity.
From a user’s perspective, the Workload Manager provides the ability to request precise computational resources without needing to know which specific rack or server they will occupy.

Explained are the features present in a Slurm Cluster:

{% endif %}

```{figure} ./../_static/clusterFeatures.png
:alt: powerWall
:width: 100%
```
{% if page %}

### Storage Architecture

In an HPC Cluster, storage is not a monolithic entity, neither is it restricted to the available disk space on the specific compute node where a job lands. Instead, it is split into distinct hierarchies addressing different persistence and performance needs:

**Shared Home Directory (Ceph):**
This is the default entry point for any user logging into the system.
In this shared setup, the user's home directory is hosted on a central storage cluster (typically backed by Ceph or a similar distributed filesystem).
This filesystem is mounted across every single node—Head and Compute alike.
This ensures that configuration files, source code, and lightweight virtual environments are instantly available regardless of where a job is scheduled to run.
However, similar to cloud shared storage, every read/write operation travels through the network, making it suboptimal for heavy I/O operations during processing.

**Shared Scratch Storage:**
For data-intensive operations, the cluster provides a "Scratch" folder, which is also a shared resource accessible from all nodes.
Unlike the Home directory, this storage is engineered for high-throughput and low-latency access, often utilizing parallel file systems like Lustre or GPFS.
It serves as the staging area for massive datasets and intermediate results during active computation.
While it offers superior speed, it is typically volatile; data residing here is often subject to automated purging policies once the associated job or project timeline concludes.

### Job Scheduling and Resource Management

The defining feature of the Slurm scheduler is the granular control over resource allocation, allowing for the execution of anything from a single core process to massive parallel simulations.

**Flexible Resource Allocation:**
A single job submission allows for the specific request of resources, ranging from a single CPU core to multiple full nodes equipped with GPU accelerators.
This flexibility allows for the precise tailoring of hardware to the code's requirements (e.g., requesting 4 GPUs and 128GB of RAM for a deep learning model).
This flexibility, however, presents a scheduling challenge: the more specific and massive the resource request, the longer the job may sit in the pending queue waiting for that exact combination of hardware to become available.

**Job Arrays and Management:**
For tasks requiring high throughput—such as hyperparameter tuning or processing thousands of individual data files—Slurm implements Job Arrays.
Instead of manually submitting hundreds of individual jobs, a single array definition spawns multiple "tasks" that share the same resource requirements but operate on different input data.
This allows the scheduler to manage thousands of processes as a single logical unit, filling available gaps in the cluster's capacity efficiently.

### Monitoring and Visibility

Slurm provides deep visibility into the state of the cluster, offering monitoring capacities that extend beyond simple pass/fail reporting.
Users can query the exact state of the queue, inspecting why a job is pending (e.g., "Resources" or "Priority").
Furthermore, it allows for the attachment to running processes to monitor standard output (stdout) and error logs in real-time.
This management layer ensures that users can track the efficiency of their allocations, verifying that the requested CPUs and GPUs are being fully utilized rather than sitting idle.

{% endif %}

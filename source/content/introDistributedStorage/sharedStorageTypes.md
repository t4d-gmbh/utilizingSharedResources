## Types of Cloud Storage

{% if slide %}

{% else %}

Modern computing infrastructures, like clouds (e.g. OpenStack) or HPC clusters running Slurm, rely on a sophisticated configuration of resources.
Most prominently, powerful CPUs and GPUs providing exaflops of performance[^1] and high-speed networks acting as the nervous system.
Less visible, but equally important is the robust strategy to store and access data.

[^1]: <https://en.wikipedia.org/wiki/TOP500>

In distributed systems, storage is often present in multiple distinct tiers, and understanding the differences between them is not just an architectural detail — it is a crucial competency.

Choosing the wrong storage type can not just mean your job runs slowly; it can starve your GPUs, waste expensive compute credits, and even severely affect the performance of an entire cluster.

Selecting an inappropriate storage type can create significant performance bottlenecks, waste computational resources, and lead to the "Noisy Neighbor" effect, where inefficient I/O operations (such as unzipping millions of small files on a parallel filesystem designed for streaming) degrade performance for all users on the cluster.

To make good use of such infrastructures and help to maintain system stability, four primary storage architectures should be understood:

- **Block Storage**
- **Object Storage**
- **Persistent Shared Filesystems**
- **Ephemeral Storage**


### Object Storage
```{admonition} "Infinite Bucket" 
:class: tip, margin
Simply toss in your data, neither worry about size nor file counts.
```

For massive datasets or large numbers of individual files, Block Storage becomes inefficient due to its lack of scalability and inability to be shared across multiple nodes.
Object Storage addresses this need.

Rather than organizing data in a hierarchical directory tree, Object Storage stores data as flat objects accessed via an API (such as HTTP REST), identified by a unique ID.
It is designed for durability and infinite scale rather than rapid modification; data is typically written once and read many times.
In many ecosystems, this is provided by OpenStack Swift or Ceph RGW (RADOS Gateway), which offer an S3-compatible interface.
This tier, sometimes also alled "Data Lake" serves in any sort of computational workflow.
It is a repository for raw logs, images, and archives that must be accessible from any node in the cluster but do not require instant modification.


### Persistent Shared Filesystems

```{admonition} Cloud NAS
:class: tip, margin
A standard network folder where your code lives, safe and accessible from every node like a local directory.
```

While Object Storage is efficient for automated retrieval, users and legacy applications often require the familiarity of a directory tree.
A centralized location is needed to store code, configuration files, and shared scripts that behave like a standard hard drive but remain accessible across the network.
This is the Persistent Shared Filesystem.

Often referred to as the "Home Directory," this storage layer (managed by Manila in OpenStack or CephFS in Ceph clusters) is fully POSIX-compliant.
Standard terminal commands like `ls`, `grep`, and `cp` function as expected.
The priority of this tier is reliability and data safety over raw throughput.
It ensures that changes in your home folder (`~/`) on a login node are immediately available on compute nodes.
It seamlessly handles file locking and permissions to allow collaboration without data conflicts.

### Ephemeral Storage

```{admonition} The "Scratchpad"
:class: tip, margin
Your high-speed workspace for heavy I/O, but wiped clean when the work is done.
```

Finally, a specialized storage tier exists to meet the unique demands of high-performance computing: Ephemeral Storage.
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

{% endif %}

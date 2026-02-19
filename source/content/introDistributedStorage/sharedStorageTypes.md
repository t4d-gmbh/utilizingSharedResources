## Types of Cloud Storage

{% if slide %}

**Why Storage Strategy Matters:**  
Choosing the wrong tier can starve expensive GPUs, waste compute credits, and create massive bottlenecks that degrade performance for everyone (the **"Noisy Neighbor"** effect).

**The 4 Primary Architectures:**

{% else %}

Modern computing infrastructures, like clouds (e.g. OpenStack) or HPC clusters running Slurm, rely on a sophisticated configuration of resources.
Most prominently, powerful CPUs and GPUs providing exaflops of performance[^1] and high-speed networks acting as the nervous system.
Less visible, but equally important is the robust strategy to store and access data.

[^1]: <https://en.wikipedia.org/wiki/TOP500>

In distributed systems, storage is often present in multiple distinct tiers, and understanding the differences between them is not just an architectural detail — it is a crucial competency.

Choosing the wrong storage type can not just mean slow job; it can starve GPUs, waste expensive compute credits, and even severely affect the performance of an entire cluster.

Selecting an inappropriate storage type can create significant performance bottlenecks, waste computational resources, and lead to the "Noisy Neighbor" effect, where inefficient I/O operations (such as unzipping millions of small files on a parallel filesystem designed for streaming) degrade performance for all users on the cluster.

To make good use of such infrastructures and help to maintain system stability, four primary storage architectures should be understood:

{% endif %}

::::{grid} 2
:gutter: 2

:::{grid-item-card} [Block Storage](#BlockStorage)
:class: sd-shadow-s text-center
*(The Virtual USB Drive)*
:::
:::{grid-item-card} [Object Storage](#ObjectStorage)
:class: sd-shadow-s text-center
*(The Infinite Bucket)*
:::
:::{grid-item-card} [Shared Filesystems](#SharedFilesystems)
:class: sd-shadow-s text-center
*(The Cloud NAS)*
:::
:::{grid-item-card} [Ephemeral Storage](#EphemeralStorage)
:class: sd-shadow-s text-center
*(The Scratchpad)*
:::
::::

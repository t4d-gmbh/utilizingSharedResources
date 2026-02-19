### Block Storage

:::{admonition} Virtual USB Drive
:class: tip, margin
{% if slide %}
Can be "plugged in" everywhere.
{% else %}
Think of Block Storage as a raw, unformatted USB drive that is plugged permanently into a single specific computer.
{% endif %}
:::
{% if slide %}
```{compound}
{.centered}
Exclusive, highly compatible virtual hard drive for fast I/O.
```
{% else %}

At the most fundamental level, every virtual machine or compute node needs a "local disk" to boot the operating system and run applications.
This is **Block Storage**.

In a cloud environment like OpenStack, systems like Cinder (often relying on **Ceph RBD**) carve out these virtual drives from a massive pool of disks.
The defining characteristic of Block Storage is exclusivity: a block volume is typically attached to **only one node at a time**.
This exclusivity allows for fast and low-latency access, making it the perfect home for your Operating System, your local software libraries (like Conda environments), and high-performance databases (like PostgreSQL) that require transactional integrity.


#### Architecture

{% endif %}



::::{grid}
:gutter: 2

{% if page %}
:::{grid-item}
:columns: 6
:class: sd-m-auto



Block Storage is handled by a storage cluster, connecting multiple storage devices (computer) together as a single unit.
A common, open-source software that can create a storage cluster on top of connected computers is [Ceph](https://ceph.io).
In Block Storage Ceph splits up a block into fixed-size junks (e.g., 4MB) that are then distributed in a redundant manner (usually 3 copies of each block) across the physical disks in the storage cluster.

{% endif %}


:::
:::{grid-item}
:columns: {% if page %}6{% else %}12{% endif %}
:class: sd-m-auto

```{image} ./../_static/blockStorage.png
:alt: BlockStorage
:width: 100%
```

:::
::::


#### Usage

{% if slide %}
{.smaller}
- Attach the volume (i.e. block) via GUI/SDK
- Partition it `parted /dev/sdX mklabel gpt`
- Cerate a filesystem `mkfs.ext4 -L mylabel /dev/sdxY`
- Mount the filesystem `mount /dev/sdxY /mnt/mydisk`

{% else %}

In a OpenStack cloud, Block Storage is managed by an application called _Cinder_.
When a volume is requested, Cinder talks to the backend (like Ceph) to reserve the blocks and attaches them to to the target VM via iSCSI or KVM virtio.

:::{admonition} `rbd` Example
:class: margin tip
Creating a new block:
```
rbd create mydisk --size 100G
```
:::

A machine, virtual or not, can also interface directly with a Ceph Block Storage via a kernel module called `rbd`.
In a virtualized environment this can be done directly form a VM or, if access allows it, on the Hypervisor which can then "present" the block storage to the VM as a physical, physical disk.
In practice, attaching a block storage via Cinder, the Hypervisor or directly on the VM using `rbd` should show little to not difference in terms of performance.

Once a block is added to a machine, it becomes visible as a device (e.g. under `/dev/sdX`).
In most cases this device will be used as filesystem, so it first needs to be (or should be) partitioned using tools like `fdisk`, `gdisk` or `parted`, and then a filesystem needs to be added (e.g. with `mkfs`).
Finally, the filesystem need to be mounted so that it can be used (use `mount` for one-time mounts and add an entry to `/etc/fstab` for permanent mounting).

{% endif %}

#### Use Cases

{% if slide %}
::::{grid} 12 12 4 4
:gutter: 1

:::{grid-item-card} Databases
:class: sd-shadow-s
:::
:::{grid-item-card} Persistent Volumes
:class: sd-shadow-s
:::
:::{grid-item-card} High-Speed Scratch
:class: sd-shadow-s
:::

::::

{% else %}

**Databases**:  
Hosting a PostgreSQL or MySQL database that requires low-latency, transactional write performance.

**Persistent Volumes**:  
Keeping OS settings and installed libraries (Conda environments) safe even if the VM is terminated.

**High-Speed Scratch**:  
"Checking out" a specific dataset to a fast, temporary drive for intense processing (e.g. on a single GPU node).

#### Pros \& Cons

{% endif %}

| Pros | Cons |
| -------------- | --------------- |
| **Lowest Latency**{% if page %}:<br>No protocol overhead (like HTTP or NFS); practically as fast as local disk.{% endif %} | **Not Shared**{% if page %}:<br>Cannot be mounted on two nodes simultaneously (without a complex cluster-aware filesystem).{% endif %} |
| **Compatibility**{% if page %}:<br>Works with any application (it's just a POSIX disk to the OS).{% endif %}| **Management**{% if page %}:<br>The user is responsible for formatting, partitioning, and filesystem repair (`fsck`).{% endif %}|



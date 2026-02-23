## Virtualization

{% if slide %}
:::::{grid} 2
::::{grid-item-card} <i class="fas fa-layer-group"></i> The Concept
- **Abstraction**: Decoupling software from hardware.
- **Partitioning**: Running multiple OSes on one physical machine.
- **Isolation**: Fault and security containment.
::::

::::{grid-item-card} <i class="fas fa-microchip"></i> The Parts
- **Cloud Operating System**: Orchestrator pooling resources across multiple hosts.
- **Hypervisor**: The software layer creating VMs.
- **Guest**: The virtualized system.
- **Host**: The underlying physical hardware.
::::
:::::

{% else %}

:::{admonition} Definition
:class: margin
Virtualization is the process of creating a virtual (rather than actual) version of computer infrastructure.
This can include virtual computer hardware platforms, storage devices, and computer network resources.
:::

{% endif %}

{% if page %}
Virtualization is the fundamental principle behind modern cloud computing infrastructures.
It enables partitioning a single physical machine (a **Host**) into multiple virtual environments (**Guests** or **Virtual Machines**).

For a computational scientist, virtualization allow to declare (almost) completely reproducible environments.
Instead of writing code that only runs on your specific laptop's hardware configuration, you target a virtual standard that can exist anywhere.

{% endif %}

{% if slide %}:::{card}{% else %}###{% endif %} <i class="fas fa-check-circle"></i> Core Benefits
{% if slide %}
1.  **Resource Efficiency**: Utilization of physical hardware increases drastically.
2.  **Isolation**: A crash in one VM does not affect others or the host.
3.  **Reproducibility**: Encapsulate the entire experimental environment (OS, libraries, code) enabling peer review and long-term archiving.
4.  **Legacy Support**: Run outdated applications on a modern infrastructure.
:::
{% else %}

Virtualization fundamentally transforms hardware usage by maximizing resource efficiency; rather than leaving powerful hardware idle, multiple workloads can be stacked on a single machine, often drastically increasing utilization.
In addition to this consolidation, an isolation between the virtualized resources ensures that crashes and security failures in one environment remain contained, leaving others unaffected.

Furthermore, virtualization drastically facilitates reproducibility: It allows for encapsulation of entire setups — OS, libraries, and code — into a portable format.
In a research context this guarantees identical results for peer review and long-term archiving.

Finally, it provides legacy support, enabling the execution of outdated but essential software on modern infrastructure without compatibility issues.
{% endif %}

### Hypervisor

The Hypervisor is the software that creates and runs virtual machines.

{% if page %}
#### <i class="fas fa-server"></i> Types of Hypervisors
{% endif %}


{% if slide %}
:::::{grid} 2
::::{grid-item}
**Type 1 (Bare Metal)**
- Runs directly on hardware.
- **High Performance**.
- *Ex: KVM, Xen, ESXi.*
::::

::::{grid-item}
**Type 2 (Hosted)**
- Runs as an app on an OS.
- **High Overhead**.
- *Ex: QEMU, VirtualBox, VMWare Workstation.*
::::
:::::
{% endif %}

{% if page %}

There are two main categories of hypervisors relevant to research:

#### Type 1: Bare Metal
These run directly on the system hardware without an underlying operating system.
They are highly efficient and are used in HPC centers and cloud providers (AWS, Azure).
* **Use Case**: Setting up a permanent server for your lab group.

#### Type 2: Hosted
These run as software applications on top of a conventional operating system (like Windows or macOS).
They abstract the guest operating system from the host operating system.
* **Use Case**: Testing a Linux workflow on your personal MacBook using VirtualBox before deploying it to the cluster.

### VMs vs. Containers
{% endif %}


{% if slide %}
:::::{grid} 2
::::{grid-item-card} <i class="fas fa-desktop"></i> Virtual Machines
- **Full Isolation**: Entire OS kernel per instance.
- **Heavy**: GBs in size, slow boot.
- **Secure**: Hard boundary.
::::

::::{grid-item-card} <i class="fas fa-box-open"></i> Containers
- **Shared Kernel**: Uses Host OS kernel.
- **Lightweight**: MBs in size, instant start.
- **Efficient**: Near-native performance.
::::
:::::
{% endif %}


{% if page %}

While **Virtual Machines (VMs)** virtualize the *hardware*, **Containers** (like Docker) virtualize the *Operating System*.

#### The Difference Matters


1. **VMs (Virtual Machines)** include the application, the necessary binaries/libraries, and an entire guest operating system.
   This makes them heavy (gigabytes) but completely independent.
   On the other hand, working with a VM feels much like working with your own laptop or desktop PC.
2. **Containers** include the application and all of its dependencies, but share the OS kernel with other containers.
   They run as isolated processes in userspace.
   Working with container can be a bit more challenging as inspection, logging and debugging can be less accessible.

#### Scientific Relevance
In modern HPC, **Containers** (often Singularity/Apptainer rather than Docker due to security) are preferred.
They allow you to package your specific Python environment, libraries, and code into a single file that runs at near-native speed on the supercomputer, guaranteeing that your results are reproducible regardless of the cluster's underlying updates.
{% endif %}

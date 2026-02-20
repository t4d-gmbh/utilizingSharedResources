## Virtualization

{% if page %}

Virtualization - **Hardware Virtualizaton** to be more precise - is the key concept in a cloud infrastructure.
It became broadly available for the standard x86 computer architecture in the early 2000s and lead to a profound change in how computer infrastructures were utilized.

The most common form, Hardware Virtualization, aims to decouple Operating System (OS) and applications from the physical hardware by providing an abstraction layer, mimicking real hardware to the virtualized Operating System.

This software (i.e. the abstraction layer) is called **Hypervisor** and intercepts communication between the OS and the computer.
A Hypervisor provides the OS with all the information and interfaces the underlying hardware typically would, leading the OS to "believe" that it runs directly on hardware.
The advantage of such a softer buffer between OS and computer comes from the flexibility that it allows in the declaration of the hardware specifications to the OS:
A Hypervisor can report only a fraction of the actual hardware to the OS, effectively hindering the OS from accessing all physically available resources.
This ultimately enables a single computer to host multiple (virtualized) Operating Systems, allowing for a better utilization of the hardware.

From a users perspective a virtualization layer allows to spawn up a OS with customized resources available.
In addition the virtualization layer allows to create snapshots of the (virtualized) Operating System that can be stored, shared and duplicated easily.

There exist multiple Hypervisor software products and not all work identically.
A common classification is to distinguish between Type 1 and Type 2 Hipervisors.

{% else %}

```{epigraph}
{.centered}
Hardware Virtualization decouples the OS from the physical hardware with an abstraction layer (Hipervisor), mimicking real hardware to the OS.  
```

{% endif %}


```{margin}
{.smaller}
_Adapted from <https://en.wikipedia.org/wiki/File:Hyperviseur.svg>_
```

::::{grid}
:gutter: 3

:::{grid-item}
:column: 6
:class: sd-m-auto

{% if slide %}

**Type 1 Hipervisor**: Acts as (host) OS.

**Type 2 Hipervisor**: Runs as application in a (host) OS.

{% else %}

**Type 1 hypervisors** are also called _native_ or _bare-metal_ hypervisors and run directly on the hardware of the host.
In a way they are the OS that runs actually on the host.
Commonly known are KVM, Xen or VMware ESXi.

**Type 2 hypervisors** (or _hosted_ hipervisors), on the other hand, run on top of an OS.
Type 2 hypervisors can be installed just like one would install an application and usually provide a graphical interface for managing virtualaized OSs.
Commonly known are VirtualBox, Parallel Desktop (MacOS only) and GNOME Boxes.

{% endif %}

:::
:::{grid-item}
:columns: 6
:class: sd-m-auto

```{image} ../_static/hypervisor.png
:alt: Hypervisor
:name: Hypervisor
:width: 100%
```
:::

::::

### Operating-System-Level Virtualization


{% if slide %}

- Virtualizes from the kernel upwards using Namespaces and Cgroups.
- Allows for fast, isolated, portable guest OS "containers".

{% else %}


Operating-system-level virtualization is a widely used architectural principle in modern infrastructure.
Unlike hardware virtualization, which simulates physical hardware to run multiple distinct operating systems, this technique partitions a single host operating system into multiple isolated environments.

At the core of this architecture is the concept of the shared kernel.
In a traditional virtualization setup, every guest requires its own full OS kernel to manage memory and hardware drivers, which creates significant overhead in terms of storage and startup time.
In contrast, OS-level virtualization leverages the existing kernel of the host machine to run multiple "guests" simultaneously.
This removes the need for an additional layer of heavy system software, allowing the environments to start in milliseconds rather than minutes.

To ensure stability and security, the host kernel creates isolated User Spaces — virtualized instances of the operating system's memory and process environment.
This isolation is achieved through two key kernel features:

**Namespaces (Isolation of View)**:  
These act as a visual filter, tricking the processes inside the virtualized environment into believing they are the only ones running on the system.
The environment sees its own independent file system, network stack, and process tree (often perceiving its main process as "Process ID 1"), while remaining blind to the host's other processes.

**Control Groups (Isolation of Resources)**:  
Often referred to as "cgroups," these enforce strict resource limits.
They ensure that a specific isolated environment can only consume a defined amount of CPU, RAM, or Disk I/O, preventing any single instance from exhausting the host's resources.

The result is a Virtual Execution Environment: a lightweight, portable unit that bundles an application with all its dependencies.
While it relies on the host kernel for execution, to the application running inside, it appears to be a fully independent operating system.



{% endif %}




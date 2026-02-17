## Virtualization

{% if page %}

Virtualization is the key concept in a cloud infrastructure.
It became broadly available for the standard x86 computer architecture in the early 2000s and lead to a profound change in how computer infrastructures were utilized.

The most common form, Hardware Virtualization, aims to decouple Operating System (OS) and applications from the physical hardware by providing an abstraction layer, mimicking real hardware to the virtualized Operating System.

This software (i.e. the abstraction layer) is called **Hypervisor** and intercepts communication between the OS and the computer.
A Hypervisor provides the OS with all the information and interfaces the underlying hardware typically would, leading the OS to "believe" that it runs directly on hardware.
The advantage of such a softer buffer between OS and computer comes from the flexibility that it allows in the declaration of the hardware specifications to the OS:
A Hypervisor can report only a fraction of the actual hardware to the OS, effectively hindering the OS from accessing all physically available resources.
This ultimately enable a single computer to host multiple (virtualized) Operating Systems, allowing for a better utilization of the hardware.

From a users perspective a virtualization layer allow to spawn up a OS with customized resources available.
In addition the virtualization layer allows to create snapshots of the (virtualized) Operating System that can be stored, shared and duplicated easily.

There exist multiple Hypervisor software products and not all work identically.
A common classification is to distinguish between Type 1 and Type 2 Hipervisors.

{% else %}

```{epigraph}
{.centered}
Hardware Virtualization decouples the OS from the physical hardware with an abstraction layer (Hipervisor), mimicking real hardware to the OS.  
An instance of a virtualized OS is typically called a **Virtual Machine**.
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

{% if slide %}

### Containers

- Operating-system-level virtualization (from the kernel up).
- Allows for fast, isolated, portable guest OS "containers".

{% else %}

Other forms of virtualization are Desktop and Operating-system-level virtualization.

In Operating-system-level virtualization is better known as **Containerization** and a widely used practice.
In containerization the kernel of the hosting OS allows multiple user-spaces (virtualized memory address space) to co-exist.
On such an user-space we can put everything from the kernel upward of an Operating System, creating a guest OS, or  "container", runs on the kernel of the hosting OS but has only selective access to resources.

**Desktop virtualization** ...



{% endif %}




## Infrastructure as a Service


```{figure} ../_static/IaaS.png
---
figclass: margin-caption
alt: IaaS
name: IaaS
{% if page %}
width: 100%
figclass: margin
{% else %}
width: 60%
{% endif %}
---
```
{% if slide %}

::::{grid} 1 1 2 2
:gutter: 3

:::{grid-item-card} Principle
:class: sd-m-auto
Computing resources are **virtualised** and **made available on demand**.  

Virtualisation separates OS (and up) from hardware.  

Usage as with a physical server.  
:::

:::{grid-item-card} Advantages
- Provides dedicated machines on demand
- Allows management of entire OS
- Provides interfaces to WWW
:::

::::

{% else %}

This model provides fundamental computing resources, such as virtual computers, block storage, and networking, in a fully virtualized manner.
Ideally, it offers the user full administrative control (root access) from the operating system upward, creating the impression of maintaining a dedicated, private machine.

This approach allows for the usage of computers on demand without the need to purchase or maintain physical hardware.
The virtualization layer enables flexible resource scaling, instant backups of entire machines (snapshots), and the easy sharing of data across resources.

In science, IaaS serves as a on-demand multi-purpose computer.
Unlike rigid supercomputing clusters, IaaS allows researchers to:

- **Ensure Reproducibility**: Spin up Virtual Machines (VMs) with specific, legacy operating systems to run older scientific code that might break on modern clusters.

- **Host Science Gateways**: Run web servers, databases, and APIs that allow the global community to access and interact with research data.

- **Perform Interactive Analysis**: Launch powerful, persistent workstations for exploratory data analysis (EDA) that do not require waiting in a batch queue.

{% endif %}


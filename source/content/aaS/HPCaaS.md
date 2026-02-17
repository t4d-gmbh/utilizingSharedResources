## HPC as a Service

```{margin}
{.smaller}
HPC = High Performance Computing
```

```{figure} ../_static/HPCaaS.png
---
figclass: margin-caption
alt: HPCaaS
name: HPCaaS
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
Computing resources are orchestrated by a controller.  

Controller collects jobs from users, schedules and batch-distributes them.  
:::

:::{grid-item-card} Advantages
- Provides (massive) comoputing power on demand
- Requires no management
- Enforces faire usage
:::

::::

{% else %}

In High Performance Computing (HPC), multiple independent computers (referred to as "nodes") are aggregated to act as a single system, enabling concurrent (parallel) and distributed processing at a massive scale.

The resulting clusters — also referred to as supercomputers, or high performance computers — form the backbone of modern research infrastructure and have become a cornerstone of advanced IT, particularly in the training of Artificial Intelligence models.

To build a performant cluster, HPC relies heavily on ultra-low latency communication between nodes.
Consequently, specialized high-speed interconnects (networking) are just as critical to the system's speed as the processors themselves.

In this ecosystem, the network acts as the central nervous system.
Unlike standard cloud computing, where web servers operate independently, HPC workloads are often tightly coupled.
If one node in a 1,000-node simulation is delayed by a fraction of a millisecond, the entire simulation stalls.
Thus, HPC is not just about raw calculation speed; it is about the synchronized harmony of computation.

High Performance Computers play a crucial role in computational science and serve as a source of discovery for phenomena that are:

- Too large (e.g., simulating the collision of galaxies).
- Too small (e.g., modeling quantum interactions between electrons).
- Too slow (e.g., modeling climate change over the next 100 years).


{% endif %}


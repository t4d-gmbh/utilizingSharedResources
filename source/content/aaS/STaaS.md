## Storage as a Service


```{figure} ../_static/STaaS.png
---
figclass: margin-caption
alt: STaaS
name: STaaS
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
Abstract physical complexity of storage with a software layer.  

Implement redundancy and high-availability into the software layer.
:::

:::{grid-item-card} Advantages
- **Decouples storage** from computational resources
- Provides **standardized interfaces**
- Brings **redundancy**, **scalability** and **high-availability**
:::

::::

{% else %}

Storage as a Service (STaaS) changes data management by decoupling storage capacity from individual compute nodes.
Instead of managing physical disks attached to servers, users consume storage as a flexible, on - demand utility — much like electricity.
Also here, the principle is to abstract the physical complexity of hard drives, RAID controllers, and redundancy is hidden behind a software layer, allowing the system to present a unified pool of infinite capacity.
For STaaS to function effectively, it relies heavily on high-performance networking, as data must travel instantly between the storage pool and the compute nodes without inducing latency that would starve the processors.

This model represents a major technological shift from Hardware-Defined to Software-Defined Storage (SDS).
Historically, large-scale storage relied on rigid, proprietary Storage Area Networks (SAN)—expensive, monolithic hardware arrays that were difficult to scale.
Today, modern infrastructure has pivoted to software solutions like Ceph, which run on standard "commodity" servers.
Ceph aggregates these generic servers into a self-healing cluster, using intelligent algorithms to distribute data.
This allows administrators to scale storage from terabytes to exabytes simply by adding more standard servers, without ever taking the system offline.


{% endif %}



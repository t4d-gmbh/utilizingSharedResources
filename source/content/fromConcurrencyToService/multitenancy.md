## Multitenancy

:::{admonition} Tenant
:class: margin tip
Independent user or organization that shares a computing system with others while maintaining logical isolation.
:::

:::{figure} ./../_static/multitenancy.png
:alt: to multitenancy
:width: 100%
{% if page %}:figclass: margin{% endif %}
:::

{% if page %}

Aside from an increased efficiency, concurrency "deserializes" the multi-purpose nature of computer systems, allowing multiple independent programs to progress simultaneously rather than sequentially.

In doing so, concurrency offers users the capability "multi-tasking", enabling a single system to execute various, potentially unrelated tasks at the same time.
However, as computer architectures grow in complexity by often incorporating highly specialized circuits for specific operations (e.g., GPUs for parallel processing) it becomes increasingly rare for a single program to fully saturate all available system resources continuously.

This creates the risk of under-utilization.
High-performance hardware represents a significant capital investment; if these specialized components are left idle because a single program cannot use them, the cost-efficiency of the system drops drastically.

Conversely, across the computing landscape, many users share nearly identical hardware requirements for their distinct workloads.

Given these two factors, the difficulty of saturating hardware with one task, and the ubiquity of similar hardware needs, one obvious mode of use for complex systems is **Multitenancy**.

{% endif %}


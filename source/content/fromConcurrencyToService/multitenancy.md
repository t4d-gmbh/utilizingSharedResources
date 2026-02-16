## From Concurrency to Multitenancy

{% if slide %}
{% else %}
{% endif %}

Aside from an increased efficienty, concurrency "deserializes" the multi-purpose nature of computer systems, allowing multiple independent programs to progress simultaneously rather than sequentially.

In doing so, concurrency offers users the cabability "multi-tasking", enabling a single system to execute various, potentially unrelated tasks at the same time.
However, as computer architectures grow in complexity - often incorporating highly specialized circuits for specific operations - it becomes increasingly rare for a single program to fully saturate all available system resources continuousely.

This creates the risk of under-utilization.
High-performance hardware represents a significant capital investment; if these specialized components are left idle because a single program cannot use them, the cost-efficiency of the system drops drastically.

Conversely, across the computing landscape, many users share nearly identical hardware requirements for their distinct workloads.

Given these two factors — the difficulty of saturating hardware with one task, and the ubiquity of similar hardware needs — one obvious mode of use for complex systems is **Multitenancy**.

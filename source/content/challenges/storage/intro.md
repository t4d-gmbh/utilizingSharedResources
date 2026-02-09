{% if build == "slides" %}
### Storeage Limitations
{% else %}
## Storage Limitations
{% endif %}

{% if slide %}
**Physical and logistical constraints affect how we store and access data**

:::::{grid} 2
::::{grid-item-card} Non-volatile Storage
- Persistent but limited capacity
- Cost scales with size and performance
::::

::::{grid-item-card} Volatile Storage (RAM)
- Fast but expensive and limited
- Determines maximum dataset size
::::
:::::
{% endif %}

{% if page %}
Storage challenges arise from fundamental physical and economic constraints in how data is persisted and accessed.

#### Non-volatile Storage Limitations

Persistent storage, whether hard drives, SSDs, or network storage, has finite capacity. Each research group operates within allocated quotas because storage infrastructure requires physical space, power, and maintenance. High-performance storage systems that can handle concurrent access from many users are particularly expensive.

Additionally, data retention policies and backup requirements effectively multiply storage needs. A dataset that occupies 1TB might require multiple TBs when accounting for backups and versioning.

#### Volatile Storage Constraints

RAM limitations often represent the practical bottleneck in data processing. While modern systems may have substantial memory, the amount required for large-scale analysis can exceed available resources. 
This is particularly acute when:

- Datasets exceed available RAM, requiring out-of-core processing strategies
- Multiple processes compete for memory on shared systems
- Data structures in memory are larger than the raw data (e.g., sparse matrices, intermediate results)

The economic reality: RAM is significantly more expensive per byte than persistent storage, limiting how much can be made available.
{% endif %}

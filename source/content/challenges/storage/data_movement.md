{% if build == "slides" %}
## Accessibility and Data Movement
{% else %}
### Accessibility and Data Movement
{% endif %}

:::{admonition} Key Terms
:class: margin
**Latency**: Time delay to access data  
**Throughput**: Volume of data transferred per unit time
:::

{% if slide %}
**Where data lives affects how you can use it**

- **Network bandwidth**: Moving terabytes takes time
- **Physical proximity**: Data locality matters (latency, throughput)
- **Access patterns**: Random vs sequential differs drastically

{% endif %}

{% if page %}
Data accessibility depends on both network infrastructure and physical proximity. Transferring large datasets across networks faces bandwidth constraints that can make certain workflows impractical. A multi-terabyte dataset that takes days to transfer may make remote processing infeasible.

Physical storage architecture affects performance significantly. Data stored on local SSDs provides dramatically different access patterns compared to network-attached storage. Random access patterns can be hundreds of times slower on spinning disks compared to sequential reads.

These realities mean that where data resides relative to computation becomes a critical design decision. Sometimes the optimal strategy is to move computation to the data rather than data to the computation.

{% endif %}

{% if slide %}

---

:::{admonition} The Data Movement Problem
:class: warning
Sometimes it's faster (and more practical) to ship a hard drive than transfer over the network
:::

{% endif %}

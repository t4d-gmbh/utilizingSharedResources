{% if build == "slides" %}
## Working with Large Datasets
{% else %}
### Working with Large Datasets
{% endif %}

{% if slide %}
**Large datasets create processing challenges**

:::::{grid} 2
::::{grid-item-card} Loading Time
- Reading from storage takes time
- Parsing and validation add overhead
- Multiple passes multiply delays
::::

::::{grid-item-card} Memory Constraints
- Dataset may not fit in RAM
- Requires streaming or batching
- Increases complexity
::::
:::::

{% endif %}

{% if slide %}

---

**Additional Considerations**

- Data preprocessing becomes a significant phase
- May need specialized formats (HDF5, Parquet, Zarr)
- Indexing strategies become critical

{% endif %}

{% if page %}
Large datasets introduce challenges beyond simple storage capacity. The time required to load, parse, and validate data becomes significant. A dataset that takes an hour to load means every experimental iteration includes that overhead.

When datasets exceed available RAM, processing strategies must change fundamentally. Instead of loading everything into memory, you need streaming approaches or batch processing. This increases code complexity and may limit which algorithms can be applied.

Data format choices become critical at scale. Plain text formats (CSV, JSON) may be convenient for small data but become impractical at larger scales due to parsing overhead and storage inefficiency. Binary formats optimized for scientific computing ([HDF5](https://en.wikipedia.org/wiki/Hierarchical_Data_Format), [Parquet](https://en.wikipedia.org/wiki/Apache_Parquet), [Zarr](https://en.wikipedia.org/wiki/Zarr_(data_format))) provide better performance but add complexity.

Effective indexing strategies can make the difference between practical and impractical workflows. Without proper indexing, finding specific subsets of data requires scanning the entire dataset.
{% endif %}

:::{admonition} Indexing
:class: margin
Creating data structures that enable fast lookup and retrieval of specific subsets without scanning the entire dataset. Similar to a book index that lets you jump directly to relevant pages.
:::
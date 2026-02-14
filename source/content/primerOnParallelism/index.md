# Primer on Parallelism

{% if build == "slides" %}

```{toctree}
:maxdepth: 3

./conceptualFramework
./architectureLevels
./implementationApproaches
./pythonParallelism
./profilingDebugging
```

{% else %}

Parallelism is central for carrying out resource and/or data intensive computations. This section provides a practical introduction to parallel computing concepts, architectural levels, and implementation strategies, with a particular focus on Python-based workflows.

Understanding how to effectively distribute computational workloads across multiple processing units—whether cores, processors, or machines—is essential for modern scientific computing. This primer covers:

- The conceptual foundations of parallel and concurrent computing
- Different architectural levels where parallelization can occur
- Practical implementation approaches: multi-threading vs. multi-processing
- Python-specific considerations and constraints
- Tools and techniques for profiling and debugging parallel code

```{include} ./conceptualFramework.md
```

```{include} ./architectureLevels.md
```

```{include} ./implementationApproaches.md
```

```{include} ./pythonParallelism.md
```

```{include} ./profilingDebugging.md
```

{% endif %}

# Primer on Parallelism

{% if build == "slides" %}

```{toctree}
:maxdepth: 3

./implementationApproaches
./pythonParallelism
./profilingDebugging
```

{% else %}

Parallelism lets you handle resource-intensive and data-heavy computations. This section covers the basics: what parallelism is, where it happens, and how to implement it (in Python).


```{include} ./implementationApproaches.md
```

```{include} ./pythonParallelism.md
```

```{include} ./profilingDebugging.md
```

{% endif %}

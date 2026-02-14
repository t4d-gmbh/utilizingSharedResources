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

Parallelism lets you handle resource-intensive and data-heavy computations. This section covers the basics: what parallelism is, where it happens, and how to implement it (in Python).

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

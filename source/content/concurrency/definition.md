---
sd_hide_title: true
---
## Definition

{% if slide %}

::::{grid}
:gutter: 3

:::{grid-item}
:columns: 4
:class: sd-m-auto

```{image} ./../_static/concurrency.png
:alt: Concurrency
:width: 100%
```

:::

:::{grid-item}
:columns: 8
:class: sd-m-auto

### Concurrency
The ability of a system to progress in multiple tasks through  

- **simultaneous execution**
- **context switching**
- **coordination**
- **process control**
- **managing interactions**
- **managing resources**

:::
::::

{% else %}

:::{figure} ./../_static/concurrency.png
:figclass: margin
:alt: Concurrency
:width: 100%
:::

```{epigraph}
The ability of a system to progress in multiple tasks through simultaneous execution, context switching, coordination, process control, managing interactions and resources.
```

In other words, concurrency is the ability of a computer system to handle multiple tasks with overlapping lifetimes, rather than running them strictly one after another.
It allows a program to be decomposed into independent segments that can run in parallel, be paused, or be resumed—all without altering the final outcome.

A concurrent system efficiently utilizes its computational capacity by avoiding idle time (e.g., switching to another task while waiting for data from RAM).

{% endif %}


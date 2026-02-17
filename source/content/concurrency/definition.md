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

:::::{grid} 2
:gutter: 3

::::{grid-item-card} Sequential Approach
:::{grid-item-card} **Dataset 1:**
- Download (30 sec)
- Process (60 sec)
:::
:::{grid-item-card} **Dataset 2:**
- Download (30 sec)
- Process (60 sec)
:::
**Total: 180 seconds**
::::

::::{grid-item-card} Concurrent Approach
:::{grid-item-card} **Dataset 1:**
- Download (30 sec)
- Process (60 sec)
:::
:::{grid-item-card} **Dataset 2:**
- *Download during proc. 1*
- Process (60 sec)
:::
**Total: 150 seconds** (17% faster)
::::
:::::

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
It allows a program to be decomposed into independent segments that can run in parallel, be paused, or be resumed without altering the final outcome.

A concurrent system efficiently utilizes its computational capacity by avoiding idle time (e.g., switching to another task while waiting for data from RAM).

### Example: Data Processing Pipeline

Consider a program that needs to download and process multiple large datasets:

:::::{grid} 2
:gutter: 3

::::{grid-item-card} Sequential Approach
:::{grid-item-card} **Dataset 1:**
- Download (30 sec)
- Process (60 sec)
:::
:::{grid-item-card} **Dataset 2:**
- Download (30 sec)
- Process (60 sec)
:::
**Total: 180 seconds**
::::

::::{grid-item-card} Concurrent Approach
:::{grid-item-card} **Dataset 1:**
- Download (30 sec)
- Process (60 sec)
:::
:::{grid-item-card} **Dataset 2:**
- *Download during processing 1*
- Process (60 sec)
:::
**Total: 150 seconds** (17% faster)
::::
:::::

This illustrates how concurrency exploits natural waiting periods. While the CPU processes one dataset, the network interface downloads another, keeping both resources actively utilized rather than leaving one idle.
{% endif %}

{% endif %}


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
It allows a program to be decomposed into independent segments that can run in parallel, be paused, or be resumed without altering the final outcome.

A concurrent system efficiently utilizes its computational capacity by avoiding idle time (e.g., switching to another task while waiting for data from RAM).

### Example: Data Processing Pipeline

Consider a program that needs to download and process multiple large datasets:

{% if slide %}
::::{grid} 2
:::{grid-item-card} Sequential Execution
Download file 1 → Process file 1 →  
Download file 2 → Process file 2

**Total time:** 2 × (download + process)
:::
:::{grid-item-card} Concurrent Execution
Download file 1 → Process file 1  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;↓ Download file 2

**Total time:** download + 2 × process
:::
::::
{% else %}

**Sequential approach:**
1. Download dataset 1 (30 seconds)
2. Process dataset 1 (60 seconds)
3. Download dataset 2 (30 seconds)
4. Process dataset 2 (60 seconds)

**Total time: 180 seconds**

**Concurrent approach:**
1. Download dataset 1 (30 seconds)
2. Process dataset 1 **while simultaneously** downloading dataset 2 (60 seconds)
3. Process dataset 2 (60 seconds)

**Total time: 150 seconds** which is a 17% improvement by overlapping network I/O with computation.

This illustrates how concurrency exploits natural waiting periods. While the CPU processes one dataset, the network interface downloads another, keeping both resources actively utilized rather than leaving one idle.
{% endif %}

{% endif %}


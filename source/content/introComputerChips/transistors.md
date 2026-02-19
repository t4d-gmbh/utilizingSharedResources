## The Transistor Computer


::::{grid}
:gutter: 3

:::{grid-item}
:columns: 6
:class: sd-m-auto

{% if slide %}

First computer primarily **driven by transistors**.

It used a **magnetic drum for storage**.
{% else %}

The Manchester Transistor Computer (TC), first operational in November 1953, marked a pivotal shift in hardware engineering as the world's first computer driven primarily by transistors rather than vacuum tubes.
While much smaller, cooler, and more reliable than its valve-based predecessors, it was a hybrid transitional machine.

{% endif %}

:::

:::{grid-item}
:columns: 6
:class: sd-m-auto

```{image} ./../_static/transistor.png
:alt: sidebar image
:width: 100%
```
:::


::::

{% if slide %}

{.centered}
**Proof that solid-state technology was viable for building UTMs.**

{% else %}

It used point-contact transistors (later replaced by more reliable junction transistors) for its logic circuits and relied on a magnetic drum for storage and, initially, a few vacuum tubes to generate its clock signal.
Running at a clock rate of approximately 125 kHz, its primary historical significance was proving that solid-state technology was viable for building a Universal Turing Machine, setting the stage for the miniaturization revolution that followed.
{% endif %}

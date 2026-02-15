## The Stored-program Computer


::::{grid}
:gutter: 3

:::{grid-item}
:columns: 6
:class: sd-m-auto
```{image} ./../_static/mark1.png
:alt: sidebar image
:width: 100%
```
:::

:::{grid-item}
:columns: 6
:class: sd-m-auto

{% if slide %}

First computer to successfully **execute an internally stored program**.

Internal storage **eliminated mechanical bottleneck** when reading instructions.
{% else %}

The Manchester Mark 1 (specifically its predecessor, the "Baby," which proved the concept in 1948, with the full Mark 1 completed in 1949) was a landmark in computing history.
It was arguably the first computer that successfully executed a program stored internally in its electronic memory.

{% endif %}

:::
::::

{% if slide %}

{.centered}
**The Manchester Mark 1 could operate at roughly 100kHz.**

{% else %}

Unlike earlier machines that read instructions from external perforated tape or plugboards, the Mark 1 used Williams tubes (modified cathode-ray tubes) to store both the program and the data as patterns of charges on the screen.
This "stored-program" architecture meant the machine could modify its own instructions at electronic speeds, effectively functioning as a high-speed Universal Turing Machine.
This internal storage eliminated the mechanical bottleneck of physical tapes, transforming the computer from a fast calculator into a truly flexible, programmable processor.

{% endif %}

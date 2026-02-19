## Physical limits


::::{grid}
:gutter: 3

:::{grid-item}
:columns: 6
:class: sd-m-auto
```{image} ./../_static/meltDown.png
:alt: sidebar image
:width: 100%
```
:::

:::{grid-item}
:columns: 6
:class: sd-m-auto

{% if slide %}

Leakage current and threshold voltage **don't scale down perfectly** with size.  

At a certain scale, **power density starts to increase sharply**, generating more heat than can be removed.

{% else %}

In practice, leakage current and threshold voltage do not scale down perfectly when shrinking transistor dimensions.
Eventually, this leads to a sharp increase in power density.
This creates a paradox where making the chip smaller actually generates more intense heat per square millimeter, making it physically impossible to cool with standard methods.

{% endif %}
:::

::::

{% if slide %}

{.centered}
This phenomenon, known as the **Power Wall marked the abrupt end of the "Megahertz Arms Race"**.

{% else %}

The practical limits were reached around 2004, famously exemplified by the cancellation of Intel's Tejas and Jayhawk projects (intended to be the Pentium V).
This moment became widely known hitting the "Power Wall".
It marked the abrupt end of the "Megahertz Arms Race".

{% endif %}

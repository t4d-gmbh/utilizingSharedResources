## Challenges


{% if slide %}
::::{grid}
:gutter: 3

:::{grid-item}
:columns: 4
:class: sd-m-auto
```{image} ./../_static/singleProcess.png
:alt: Single process
:width: 100%
```
:::

:::{grid-item}
:columns: 8
:class: sd-m-auto

{.centered}
Multi-CPU microprocessors alone **do not speed up a single process**.

:::

::::
{% else %}

With Dannard scaling smaller transistors allowed to ramp up the core clock rate and with a higher clock rate a CPU would simply process instructions faster, no adaption on the programs needed.

Combining multiple CPUs onto a microprocessor, on the other hand, does not have any effect on a program that is designed to run its instructions on a single core.

Leveraging multi-CPU structures requires a complete redesign of an algorithm or program!

{% endif %}

::::{grid}
:gutter: 3


:::{grid-item}
:columns: 8

{% if slide %}
{.centered}
**In the past:**  

A "universal" microprocessors can (theoretically) already perform all operations.

Extra transistors (Moore's law) on a microprocessor can be used **to make it more efficient**.

{% else %}
### In the past

In fact, already when we look back to Moore's Law - stating that the number of transistors on a microprocessor doubles approximately every two years - we should wonder:

Why would we want to modify our UTM by adding more transistors if it is already a "universal" computer?

The reason is efficiency:  
The definition of the Turing Machine ensures _computability_ (can it be done?), but it does not include any notion of _efficiency_ (how long will it take?).

{% endif %}

:::

:::{grid-item}
:columns: 4
:class: sd-m-auto
```{image} ./../_static/efficientUTM.png
:alt: Single process
:width: 100%
```
:::

::::

{% if slide %}
{.centered}
**Allowing a program to take advantage of complexer hardware requires redesigning it!**

{% else %}


{% endif %}


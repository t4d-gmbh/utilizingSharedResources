## The <i class="fa-solid fa-microchip"></i> scaling laws


::::{grid}
:gutter: 3

:::{grid-item}
:columns: 12
:class: sd-m-auto
```{image} ./../_static/laws.png
:alt: laws
:width: 100%
```
:::
::::

{% if slide %}

::::{grid}
:gutter: 3

:::{grid-item}
:columns: 6

**Moore's Law:**  
The number of transistors on a chip doubles every two years.

:::

:::{grid-item}
:columns: 6 

**Dennard scaling:**  
Power usage of a transistor is proportional to its area.  

{.smaller}
_The clock frequency increases with decreasing size._

<!-- ; smaller transistors switch faster and use less energy. -->

:::
::::

{.centered}
**The "Golden Age":**  
**Smaller transistors lead to faster, more efficient microprocessors.**

{% else %}

Moore's Law, formulated by Gordon Moore in 1965, is the observation that the number of transistors on a microchip doubles approximately every two years.
This prediction set the pace for the entire semiconductor industry, driving a relentless pursuit of miniaturization that allowed engineers to pack exponentially more computing power into the same amount of space.

Complementing this was Dennard Scaling, formulated by Robert Dennard in 1974.
Dennard observed that as transistors get smaller, their power density stays constant, so that power use stays in proportion with area.
This critical realization meant that shrinking transistors didn't just save space; it also allowed them to switch faster while using less energy, preventing the chip from overheating even as the transistor count skyrocketed.

Together, these two principles fueled the "Golden Age" of computing, ensuring that for decades, computers became consistently faster, smaller, and cheaper all at the same time.
In addition to the speed gain, smaller transistors also allowed for more transistors on the same surface area, leading to a double benefit.
With the increasing number of transistors a redesigning diversification of the CPU started, allowing for instruction level parallelism, on-chip memory (cache) and dedicated circuits for specialized tasks, such as video and audio data processing.

{% endif %}

## The Power Wall


::::{grid}
:gutter: 3

:::{grid-item}
:columns: 12
:class: sd-m-auto
```{image} ./../_static/powerWall.png
:alt: powerWall
:width: 100%
```
{.smaller}
_Adapted from <https://en.wikipedia.org/wiki/File:CPU_clock_speed_and_Core_count_Graph.png>_
:::
::::

::::{grid}
:gutter: 3

:::{grid-item}
:columns: 12

{% if slide %}
Since \~2005 **Dennard scaling broke down in practice**.  

While they keep getting smaller, **transistors can no longer be run at their maximal potential speed**.  

{% else %}
Since ~2005, Dennard scaling has broken down in practice.
While the transistor count in integrated circuits continued to grow (and their size continued to decrease), their clock frequency stagnated.
At this scale, it is simply no longer possible to run transistors at their maximum potential speed due to thermal limits.
The era of speed gain through simple transistor scaling was over.
{% endif %}

:::
::::


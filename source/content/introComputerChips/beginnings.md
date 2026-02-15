## <i class="fa-regular fa-lightbulb"></i> Universal Turing Machine

::::{grid}
:gutter: 3

:::{grid-item}
:columns: 6
```{image} ./../_static/turing.png
:alt: sidebar image
:width: 100%
:class: sd-m-auto
```
:::

:::{grid-item}
:columns: 6
:class: sd-m-auto

{% if slide %}

**Turing Machine**:
An abstract machine capable to implement **any** algorithm.

**Universal Turing Machine (UTM)**:  
A Turing Machine capable to mimic **any** Turing Machine.

{% else %}

The **Turing machine** is a conceptual model of a machine that can, by manipulation of a memory tape according to a fixed table of rules, implement an arbitrary algorithm.
The memory tape is a linear sequence of symbols that can be read and altered by the machine, following the table of rules.
While the length of the memory tape might need to be infinite, the set of symbols it can contain, i.e. the alphabet of the machine must be finite.

{% endif %}
:::
::::

{% if slide %}

{.centered}
**With a UTM any algorithm becomes just a set of instructions.**

{% else %}
The **Universal Turing Machine** (UTM) is a Turing Machine with a fixed table of rules that can, given right memory tape, mimic any Turing Machine and thus can implement any algorithm simply by providing it with the right memory tape.

Consequentially, given an UTM, any algorithm or program can be implemented "simply" by delivering a sequence of instructions (i.e. the memory tape).
This makes an UTM a universal device for algorithmic operations that does, once created, not need to be modified ever again, even when its use case changes.
With an UTM, the process of building an arbitrary program becomes a purely logical challenge: Determine the correct set of instructions to feed to an UTM.

{% endif %}



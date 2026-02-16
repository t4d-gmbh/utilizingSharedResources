---
sd_hide_title: true
---
## Efficiency

:::{admonition} The UTM
:class: dropdown, margin, tip
The Universal Turing Machine (UTM) is theoretically capable of implementing any algorithm or program based on a sequence of instructions. Once we have a practical implementation of a (linear-bounded) Universal Turing Machine, have no need to ever change it, as it can carry out any task we can think of.
:::

::::{grid}
:gutter: 3

:::{grid-item}
:columns: 6
:class: sd-m-auto

{% if slide %}


{% else %}

Simply combining CPUs into a multi-core microprocessor does not yet make one process run faster.
In fact, already when we look back to Moore's Law - stating that the number of transistors on a microprocessor doubles approximately every two years - we should wonder:

Why would we want to modify our UTM by adding more transistors if it is already a "universal" computer?

The reason is efficiency:  
The definition of the Turing Machine ensures _computability_ (can it be done?), but it does not include any notion of _efficiency_ (how long will it take?).

{% endif %}

:::

:::{grid-item}
:columns: 6
:class: sd-m-auto

```{image} ./../_static/efficientUTM.png
:alt: Moore and UTM
:width: 100%
```
:::


::::

{% if slide %}

{.centered}
**.**

{% else %}


We modify the machine not to make it "smarter," but to make it more efficient and thus faster.

Moore's Law laid the foundation for these efforts by providing the "transistor budget" needed to add complex features.
Long before the "Power Wall" was hit in 2005 and chip producers started to combine multiple CPUs into a single integrated circuit, concurrent computing practices were already being integrated into microprocessors to boost performance:

**Instruction Level Parallelism (ILP)**:  
Techniques like Pipelining and Superscalar execution, where different stages of multiple instructions (Fetch, Decode, Execute) run simultaneously on separate parts of the chip.
This allows the CPU to process more than one instruction per clock cycle.

**Multithreading**:  
Where a single physical CPU core is designed to handle two or more software "threads" at once.
By duplicating the architectural state (registers), the CPU can switch back and forth instantly; if one thread stalls (waiting for slow memory), the other thread can jump in and use the execution units, keeping the processor busy.

When combining multiple-CPUs onto a single microprocessor these practices were complemented by:

**Multiprocessing**:
Where multiple independent processing units ("cores") are integrated onto a single physical chip.
Unlike multithreading, which shares execution resources within one core, multiprocessing provides each core with its own dedicated execution units and cache memory.
This allows the system to execute completely separate instructions or programs in true parallel, effectively multiplying the total performance without needing to increase the clock frequency.


{% endif %}



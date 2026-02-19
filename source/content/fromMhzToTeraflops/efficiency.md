<!--
---
sd_hide_title: true
---
-->
## Efficiency through complexity

{% if slide %}

**Evolution Beyond Speed**:  
Microprocessors have evolved not just for higher clock speeds but for increased complexity, using the "transistor budget" from Moore's Law to add efficiency-boosting features like on-chip memory (Cache) and specialized circuits long before the "Power Wall" was hit.

**The Power Wall & Multi-core Shift**:  
Around 2005, physical limits forced a pivot away from raw frequency increases toward multi-core architectures, meaning single-thread performance could no longer be the sole driver of speed.

**The Software Consequence**:  
This shift meant that software could no longer automatically run faster on new chips; instead, programs had to be redesigned to leverage **concurrency** to unlock the full potential of modern hardware.

{% else %}

Microprocessors have continuously evolved not just to increase clock speed, but to increase their complexity, enabling more efficient instruction processing.

Moore’s Law laid the foundation for these efforts by providing the 'transistor budget' needed to add these complex features.
Long before the 'Power Wall' was hit in 2005 (forcing the shift to multi-core), CPUs were already equipped with architectures allowing instructions to run partially in parallel (ILP), layers of on-chip memory (L1/L2/L3 Cache) for ultra-low latency, and dedicated circuits for specialized tasks.

Practically speaking, these adaptations created massive potential for efficiency. While some improvements (like Cache) sped up programs automatically, others (like specialized circuits) meant that software often needed to be redesigned to fully leverage this new potential.

With the switch to multi-core microprocessors, an efficient program could no longer rely on increasing clock speeds; instead, it needed to take advantage of the increased complexity and parallelism introduced.
The predominant paradigm for such adaptations is **Concurrency**.


{% endif %}



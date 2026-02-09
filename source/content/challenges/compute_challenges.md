{% if build == "slides" %}
# Compute Limitations
{% else %}
## Computational Constraints
{% endif %}

{% if slide %}
:::::{grid} 2
::::{grid-item-card} CPU Limitations
- Clock speed plateaued (~2005)
- Single-threaded gains diminishing
- Parallelization is key
::::

::::{grid-item-card} GPU Constraints
- Massive parallelism for suitable workloads
- High cost, limited availability
- Not all algorithms benefit
::::
:::::
{% endif %}

:::{admonition} Spinning Threads
:class: margin
Independent execution sequences within a program that can run concurrently on multiple CPU cores.
:::

{% if page %}
Computational power faces fundamental physical limits that affect how quickly calculations can be performed.

### CPU Limitations

CPU performance stopped following simple exponential growth around 2005. Clock speeds plateaued due to power and heat constraints. Moore's Law continues through increased core counts and architectural improvements, but single-threaded performance improvements have slowed dramatically.

This means that algorithms designed for sequential execution see diminishing returns from newer hardware. Performance gains increasingly require rethinking algorithms to exploit parallelism across multiple cores.

### GPU Computing Challenges

GPUs offer massive parallelism for suitable workloads, providing 10-100x speedups for some problems. However, GPUs present their own constraints:

- **Limited availability**: Shared resources with high demand, particularly for modern high-end GPUs
- **Cost**: High-performance GPUs are expensive, limiting how many can be deployed
- **Algorithm suitability**: Not all algorithms benefit from GPU acceleration. Problems requiring frequent branching, small data volumes, or complex memory access patterns may see minimal improvement
- **Programming complexity**: Effective GPU utilization often requires significant code modification

The economic reality: compute resources are finite and must be shared across many users and projects.
{% endif %}

{% if build == "slides" %}
---
{% else %}
### Specialized Hardware Requirements
{% endif %}

{% if slide %}
:::::{grid} 2
::::{grid-item}
**Hardware Needs**

- ML: Tensor cores, TPUs
- Simulation: High memory, fast interconnects
- Data: High I/O bandwidth
::::

::::{grid-item}
**The Challenge**

- Expensive to acquire
- Limited availability
- Code portability issues
::::
:::::
{% endif %}

{% if page %}
Modern computational problems increasingly benefit from specialized hardware beyond standard CPUs and GPUs:

- **Machine learning accelerators**: Tensor cores in modern GPUs, TPUs, and specialized AI chips optimize matrix operations
- **High-memory systems**: Some algorithms require extraordinary RAM capacity (terabytes) not available in standard machines
- **Fast interconnects**: Distributed computing benefits from low-latency networking (InfiniBand, specialized fabrics)

The challenge is that specialized hardware represents significant capital investment. Facilities can only provide limited quantities, creating competition for access. Additionally, code written for one specialized architecture may not work on another, creating potential lock-in or requiring multiple implementations.

Researchers must balance the performance benefits of specialized hardware against availability constraints and development complexity.
{% endif %}

{% if build == "slides" %}
---
{% else %}
### Long Runtime Challenges
{% endif %}

{% if slide %}
:::::{grid} 2
::::{grid-item-card} Why So Slow?
- Non-linear complexity (O(n²), O(n³))
- Iterative convergence
- Parameter sweeps, Monte Carlo
::::

::::{grid-item-card} Impact
- No interactive development
- Costly failures
- Different debugging strategies
- Planning overhead
::::
:::::
{% endif %}

:::{admonition} Big O Notation
:class: margin
Describes how runtime grows with input size. O(n) is linear, O(n²) is quadratic (doubles input → quadruples time)
:::

{% if page %}
Long runtimes arise from the fundamental complexity of scientific problems. Many algorithms have computational complexity that scales faster than linearly with problem size. Doubling the problem size might quadruple or increase runtime by even more.

High-accuracy simulations often require iterative refinement, where each iteration depends on previous results. Convergence may require thousands or millions of iterations. Similarly, statistical methods like Monte Carlo simulation or parameter sweeps need many repetitions to achieve reliable results.

### Practical Consequences

Long runtimes change how you work:

- **Development cycle**: You can't quickly test changes and iterate. Each modification might require hours or days to validate.
- **Cost of failure**: If a calculation fails after running for days, you've lost significant time and resources. Robust error handling becomes critical.
- **Debugging strategy**: Traditional interactive debugging doesn't work. You need logging, checkpointing, and the ability to restart from intermediate states.
- **Planning overhead**: Results aren't immediately available, requiring careful planning about what to compute and when.

These constraints push toward batch processing models, careful validation of small-scale tests before full runs, and robust automation to handle failures gracefully.
{% endif %}

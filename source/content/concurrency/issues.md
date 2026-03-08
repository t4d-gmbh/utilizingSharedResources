## Issues & Challenges

::::{grid} 1 2 2 2
:gutter: 2

:::{grid-item}
:columns: {% if slide %}6{% else %}12{% endif %}

{% if slide %}

* **Indeterminacy:** Outcomes depend on the timing of events.
* **Execution Risks:** Incorrect outcomes, deadlocks, or process starvation.
* **The Efficiency Gap:** Concurrency is only *potential* for efficiency.

**Engineering Challenges:**

* Reliable coordination of execution.
* Safe data exchange and memory allocation.
* Mitigating communication overhead.

**Implementing overlapped operations** requires:

* **Resource contention:** Shared network buffers or bandwidth limits.
* **Memory management:** Risk of overuse.
* **Indeterminate error handling:** Timing of failure detection altering program flow.
* **Coordination overhead:** Signaling mechanisms (locks, semaphores).

{% else %}

While concurrency offers massive potential for performance optimization, significant complexity and risk are introduced into the software architecture.

Because concurrent computations interact during execution, the number of possible execution paths becomes extremely large.
This can lead to **indeterminacy**, where a program's outcome is dictated by the precise timing of events rather than strict code logic.

Under such conditions, a program may produce incorrect computational outcomes, enter a deadlock, or be permanently denied necessary resources (process starvation), severely impacting reproducibility.



{% endif %}
:::
:::{grid-item-card} The Lost Update Problem
:columns: {% if slide %}6{% else %}12{% endif %}

Example:

^^^

{% if page %}
A fundamental illustration of indeterminacy is the lost update problem.
When a shared counter is incremented by multiple threads simultaneously, the expected outcome is rarely achieved:
{% endif %}

**The non-atomic increment:** `counter = counter + 1` requires three steps: Read, Add, Write.

```python
import threading

counter = 0

def increment():
    global counter
    for _ in range(100000):
        counter = counter + 1  # Read, add, write

t1 = threading.Thread(target=increment)
t2 = threading.Thread(target=increment)
t1.start(); t2.start()
t1.join(); t2.join()

print(counter)  # Expected: 200000, Actual: Indeterminate

```

{% if page %}

Executing this program multiple times produces varying, non-reproducible results (e.g., `143256`, `158432`, `127891`).

The operation `counter = counter + 1` is not atomic; it consists of three distinct machine-level operations:

1. Read the current value.
2. Add one.
3. Write the result back.

If multiple threads read the identical value before a write operation occurs, updates are overwritten and lost. Since the exact interleaving of these operations depends on unpredictable OS scheduler timing, the final result changes with each execution.
{% endif %}
:::
::::

{% if page %}
### The Efficiency Gap


Concurrency establishes the *potential* for efficient execution; it does not guarantee it.
Designing an architecture to realize this efficiency is a highly complex engineering task.
It necessitates the implementation of reliable techniques for execution coordination, data exchange, and memory allocation.

Furthermore, success is heavily dependent on the task profile: while some problems are easily decomposed into independent units, others are tightly coupled.
In tightly coupled scenarios, performance gains can easily be negated by the synchronization and communication overhead required to maintain data integrity.

### Hidden Complexity


When implementing overlapped operations, such as simultaneous data downloading and processing, several critical architectural challenges must be addressed:

* **Resource contention:** If multiple concurrent streams share the same network buffer or bandwidth limits, mutual degradation can occur, eliminating expected speedups.
* **Memory management:** Loading secondary datasets into memory while primary datasets are actively processed requires strict allocation controls. Insufficient memory leads to thrashing (excessive data swapping to disk), rendering concurrent execution significantly slower than sequential processing.
* **Indeterminate error handling:** If a secondary operation (e.g., a download) fails during primary processing, the resolution path is highly dependent on the exact timing of the failure detection. The logic required to halt, finish, or retry operations safely introduces complex state management.
* **Coordination overhead:** The processing task must be notified when a secondary dataset is ready. Implementing these signaling mechanisms (using locks, semaphores, or condition variables) introduces runtime overhead that can easily negate performance benefits, especially for smaller workloads.

{% endif %}

:::{admonition} Key Takeaway
:class: tip

{% if slide %}
The gap between conceptual simplicity and implementation complexity is characteristic of concurrent programming, requiring expertise in synchronization, resource management, and error handling.
{% else %}
While concurrent pipelines appear conceptually straightforward, implementing them correctly requires deep expertise in thread synchronization, resource management, and error handling. This gap between conceptual simplicity and implementation complexity is a fundamental characteristic of concurrent programming.
{% endif %}
:::


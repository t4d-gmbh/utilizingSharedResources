## Issues \& Challenges

{% if slide %}
Concurrenct system designs offer massive potential for perfomance, but...

- **concurrent computations are no longer independent** which can lead to **indeterminacy** (i.e. the output of a programm changes or the programm even stalls).

- to take advantage of this **a program must be designed for concurrency**, which can quickly become extremely challenging.

{% else %}

While concurrency offers massive potential for performance, it introduces significant complexity and risk:

#### Indeterminacy & Complexity
Because concurrent computations interact while executing, the number of possible execution paths can become extremely large.
This can lead to **indeterminacy**, where the program's outcome changes based on the precise timing of events rather than just the code logic.
In such cases a program can also produce wrong outcomes, run into a deadlock or be permanently denied the needed resources (process starvation).

#### The Efficiency Gap
Concurrency only creates the *potential* for a program to run efficiently; it does not guarantee it.
Actually designing a program to realize this efficiency is an extremely challenging engineering task.
It entails finding reliable techniques for coordinating execution, data exchange, and memory allocation.
Furthermore, the success depends heavily on the **type of task**: some problems are easily broken into independent pieces, while others are tightly coupled and difficult to execute concurrently without losing performance to overhead.

### Example Revisited: Hidden Complexity

Recall the data processing pipeline where we overlapped downloading with processing. While conceptually simple, implementing this correctly requires handling several challenges:

{% if slide %}
:::{admonition} Potential Issues
:class: warning
- **Shared resources:** Both downloads may compete for limited network bandwidth
- **Memory constraints:** Loading file 2 while processing file 1 requires enough RAM for both
- **Error handling:** What if download 2 fails during processing of file 1?
- **Coordination:** How does the processor know when file 2 is ready?
:::
{% else %}

**Resource contention:**  
If both downloads share the same network buffer or bandwidth limits, they may slow each other down, eliminating the expected speedup.

**Memory management:**  
Loading dataset 2 into memory while dataset 1 is still being processed requires careful allocation. If total memory is insufficient, the system may thrash (constantly swapping data to disk), making concurrent execution *slower* than sequential.

**Indeterminacy in error handling:**  
Suppose the download of dataset 2 fails while dataset 1 is being processed. Should the program:
- Stop processing immediately?
- Finish processing dataset 1, then report the error?
- Retry the download automatically?

The answer depends on program logic, but the *timing* of when the error is detected can lead to different outcomes (classic indeterminacy).

**Coordination overhead:**  
The processing task must somehow be notified when dataset 2 is ready. Implementing this signaling mechanism (locks, semaphores, condition variables) adds complexity and runtime overhead that can negate the performance benefits, especially for smaller datasets.

:::{admonition} Key Takeaway
:class: tip
The data processing example seems straightforward, but implementing it correctly requires expertise in thread synchronization, resource management, and error handling. This gap between conceptual simplicity and implementation complexity is characteristic of concurrent programming.
:::
{% endif %}

{% endif %}


## Issues \& Challenges

{% if slide %}
Concurrenct system designs offer massive potential for perfomance, but...

- **concurrent computations are no longer independent** which can lead to **indeterminacy** (i.e. the output of a programm changes or the programm even stalls).

- to take advantag of this **a program must be designed for concurrency**, which can quickly become extremely challenging.

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

{% endif %}


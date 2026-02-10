# Parallelism

*Parallel computing is a complex field, and we will not explore it in depth here. However, if this subject interests you, the Wikipedia article on [Parallel computing](https://en.wikipedia.org/wiki/Parallel_computing) serves as an excellent starting point.*

Parallel computing has become the dominant paradigm in modern computer architecture. But what does this actually entail, and what forms does it take?

In a computational context, true parallelism—progressing simultaneously—is only possible if each task executes on its own physical processing unit, known as a core or CPU. Consequently, parallel processing inherently requires a multi-core architecture.  Depending on the problem at hand, certain hardware architectures may be more suitable than others. Over time, engineers have developed a variety of architectural designs to target specific types of parallel workloads.

A standard method for classifying parallelization problems is by the frequency of information exchange required between tasks.  When tasks must exchange data many times per second, we describe it as **fine-grained parallelism**. If information flows only a few times per second, we use the term **coarse-grained parallelism**. Finally, if information exchange is rare or non-existent, it is referred to as **embarrassingly parallel**.

Designing efficient solutions for fine-grained parallelism is often difficult; the frequent need for communication risks introducing wait times, which can reduce overall efficiency. Conversely, embarrassing parallelism is generally easier to implement. This is particularly true if tasks require no information exchange, thereby eliminating the need for complex inter-process communication mechanisms (assuming parallelism occurs at the process level).

Therefore, a practical first step when considering a parallel solution is to determine if the problem fits the **embarrassingly parallel** model. If it does, implementing a parallelized solution is usually a worthwhile investment.

Source:\

* [https://en.wikipedia.org/wiki/Concurrent_computation](https://en.wikipedia.org/wiki/Concurrent_computation)\
* [https://en.wikipedia.org/wiki/Parallel_computing](https://en.wikipedia.org/wiki/Parallel_computing)\

---

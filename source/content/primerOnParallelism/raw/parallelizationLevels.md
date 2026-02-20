# Levels of parallelism

As discussed in [Process and Thread](https://www.google.com/search?q=/jump_to_id/546ce17593f2494c8d0bf37003f9f1b5), a single process containing multiple threads can achieve parallel execution only if those threads run truly simultaneously on different cores. In this scenario, multi-threading equates to parallel execution.
Because threads within a process share memory, they can exchange information efficiently. However, this shared state introduces the risk of race conditions or deadlocks.
When managed correctly, truly parallel multi-threading is a highly efficient method for solving fine-grained parallelism problems.

Languages that natively support parallelism via multi-threading include: **Rust**, **Go**, **C++**, and **Java**.
Python, as we will explore later, supports multi-threading for *concurrent* execution. However, within a standard Python process, only one thread can advance at a time.
This limitation is caused by the [Global Interpreter Lock](https://en.wikipedia.org/wiki/Global_interpreter_lock) (GIL) found in [CPython](https://en.wikipedia.org/wiki/CPython), the most common Python implementation.
Consequently, multi-threading in Python achieves concurrency, but not parallelism.

Beyond multi-threading, parallel execution can also be achieved by running multiple processes simultaneously—known as multi-processing.
As previously noted, separate processes require specific Inter-Process Communication (IPC) mechanisms to exchange data.
These mechanisms add overhead, which can reduce—sometimes substantially—the efficiency gains of parallel execution.
This overhead is particularly detrimental for fine-grained parallelism but is often negligible in embarrassingly parallel scenarios.

Ultimately, true parallelism relies on multiple physical processors communicating with varying degrees of efficiency depending on the hardware design.

The arrangement of these physical processors—the computer architecture—can vary significantly. Architectures are often classified by the level at which they support parallelism.
You are likely familiar with common classifications such as multi-core, cluster, or cloud computing.
The Wikipedia [article about parallel computing](https://en.wikipedia.org/wiki/Parallel_computing#Classes_of_parallel_computers) offers a concise list of these architectural classes.

In an academic setting, you will typically encounter:

* **Multi-core computers:** Personal devices like your laptop.
* **High-Performance Computing (HPC) clusters:** Systems like [UZH's ScienceCluster](https://zi.uzh.ch/en/teaching-and-research/science-it/computing/sciencecluster.html).
* **Cloud architectures:** Platforms like [AWS](https://en.wikipedia.org/wiki/Amazon_Web_Services) or [UZH's ScienceCloud](https://zi.uzh.ch/en/teaching-and-research/science-it/computing/sciencecloud.html).

From a practical perspective, the primary difference between these architectures is how tasks are created and how information is exchanged or gathered.
Notably, a cloud or cluster architecture is often composed of many networked multi-core computers, meaning parallelization can occur on multiple architectural levels simultaneously.

Many programming languages offer straightforward abstractions for leveraging multi-core architectures, simplifying task life-cycle management and communication.
However, in cluster or cloud environments, the landscape is more complex. Implementing parallelism here often requires additional software, such as the [slurm](https://en.wikipedia.org/wiki/Slurm_Workload_Manager) workload manager, to schedule and manage tasks across the network.

---

*Side note:*

Multi-core end-user devices, such as laptops or workstations, often list specifications like "8 CPU / 16 threads." This typically indicates a "Hyper-Threading (HT)" architecture, where a single physical core is optimized to process two threads concurrently.

It is important to understand that an 8 CPU / 16 Thread machine cannot run 16 tasks in *parallel*—it can run 8 tasks in parallel. However, it is highly efficient at *concurrently* handling two threads per physical core.
Since a thread often waits for operations other than calculation (like I/O or network traffic), running two threads on one CPU can utilize the processor's idle time, increasing overall efficiency. Additionally, managing more threads can sometimes optimize cache usage.

---

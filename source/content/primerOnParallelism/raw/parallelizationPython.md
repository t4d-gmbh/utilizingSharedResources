# Efficiency in Python

Python manages thread safety using a mechanism called the [Global Interpreter Lock (GIL)](https://en.wikipedia.org/wiki/Global_interpreter_lock). This lock ensures that while a process can spawn multiple threads capable of running concurrently, no two threads belonging to the same process can execute Python bytecodes at the exact same instant.

Because of the GIL, race conditions are effectively prevented. However, the trade-off is that a single Python process is limited to one thread of execution at any given time.
The major consequence of this architecture is that **CPU-intensive tasks** often see little to no performance gain from multi-threading.
Conversely, tasks that are **I/O-bound**—such as waiting for file operations or network responses—can benefit significantly. In these cases, the GIL is released while waiting, allowing other threads to run and utilizing the CPU more efficiently, even on a single-core machine.

## Threading vs. Multi-Processing in Python

The [threading](https://docs.python.org/3/library/threading.html) library provides a standard interface for implementing multi-threaded processes in Python.
For scenarios requiring finer control over concurrency (specifically, cooperative multitasking where the program decides when to switch tasks), asynchronous libraries like [asyncio](https://docs.python.org/3/library/asyncio.html) or [aiohttp](https://github.com/aio-libs/aiohttp) are excellent alternatives.

To achieve true parallelism on multi-core architectures, Python offers the [multiprocessing](https://docs.python.org/3/library/multiprocessing.html) module. This allows you to bypass the GIL by spawning distinct processes, each with its own Python interpreter.

To visualize the performance differences between threading and multi-processing, consider the code below:

```python
import time
import threading
import multiprocessing 

import numpy as np

import matplotlib.pyplot as plt


def report_work(t_start, array, target_index:int=1):
    """
    Function repeatedly adding the moment of its execution to a binned array.
    """
    if t_start is None:
        t_start = time.perf_counter_ns()
    dt = array[1,0] - array[0, 0]
    while True:
        since_start = time.perf_counter_ns() - t_start
        i = int(since_start/dt)
        if i >= len(array):
            # Computation is done
            break
        # report the operation in the correct bin
        array[i, target_index] += 1
    return array

def main(nbr_intervals:int=1000):
    """
    Run a workload in a signle process in a single thread
    """
    t_start = time.perf_counter_ns()
    array = np.zeros((nbr_intervals, 2), dtype=int)
    array[:, 0] = 50000 * np.arange(1, nbr_intervals + 1)
    report_work(t_start, array)
    return array

def multi_threading_main(nbr_intervals:int=1000, nbr_threads:int=4):
    """
    Run the work reporting in a signle Process in a single thread
    """
    t_start = time.perf_counter_ns()
    array = np.zeros((nbr_intervals, nbr_threads + 1), dtype=int)
    array[:, 0] = 50000 * np.arange(1, nbr_intervals + 1)
    threads = []
    for i in range(nbr_threads):
        threads.append(
            threading.Thread(target=report_work,
                             args=(t_start, array, i + 1))
        )
    for thread in threads:
        thread.start()
    for thread in threads:
        thread.join()
    return array

def multi_processed_main(nbr_intervals:int=1000, nbr_processes:int=4):
    """
    Run the work reporting in a signle Process in a single thread
    """
    array = np.zeros((nbr_intervals, 2), dtype=int)
    array[:, 0] = 50000 * np.arange(1, nbr_intervals + 1)
    multiprocessing.set_start_method('spawn')
    with multiprocessing.Pool(nbr_processes) as pool:
        arrays = pool.starmap(report_work,
                              [(None, np.copy(array), 1)
                               for _ in range(nbr_processes)])

    return arrays

if __name__ == '__main__':
    # nuber of intervals
    nbr_intervals = 2000
    # number of threads or processes
    nbr_instances = 4
    # run the simple process without multi-threading
    simple_computations = main(nbr_intervals)
    simple_nbr_iterations = np.sum(np.sum(simple_computations, axis=0)[1:])
    # run the multi-threraded process
    threaded_computations = multi_threading_main(nbr_intervals,
                                                 nbr_threads=nbr_instances)
    threaded_nbr_iterations = np.sum(np.sum(threaded_computations, axis=0)[1:])
    # run the multi-process 
    mp_arrays = multi_processed_main(nbr_intervals=nbr_intervals,
                         nbr_processes=nbr_instances)
    mp_nbr_iterations = sum([np.sum(array, axis=0)[1:][0] for array in mp_arrays])

    # Simple plot to highlight the performance
    fig, (ax1, ax2, ax3) = plt.subplots(1, 3, figsize=(12, 6), sharey=True)
    # plot simple proces
    ax1.plot(simple_computations[:, 0],
             simple_computations[:, 1])
    # plot multi-threaded process
    for i in range(nbr_instances):
        ax2.plot(threaded_computations[:, 0],
                 threaded_computations[:, i + 1])
    # plot multi-process
    for array in mp_arrays:
        ax3.plot(array[:, 0],
                 array[:, 1])

    # setting titles and things
    ax1.set_title(f"Simple process: {simple_nbr_iterations} operations")
    ax2.set_title(f"{nbr_instances} threads: {threaded_nbr_iterations} operations.")
    ax3.set_title(f"{nbr_instances} processes: {mp_nbr_iterations} operations.")
    ax1.set_ylabel('Operations per bin')
    ax2.set_xlabel('Time')
    plt.tight_layout()

    plt.savefig('./mulitprocessing_illustration.png')

```

In this script, we repeatedly execute a simple task: incrementing a counter in a time-binned array. This task is purely CPU-bound, involving no I/O operations.

We test three scenarios:

1. **Single Process:** A standard execution.
2. **Multi-threaded:** A single process spawning multiple threads.
3. **Multi-processing:** Execution split across multiple distinct processes.

Crucially, in the multi-threaded version, threads share the same memory space, allowing them to write to the same `array` object. In contrast, the multi-processing version requires that each process receives its own copy of the array; processes cannot directly access or modify each other's memory.

The resulting performance is visualized below:

The results are revealing. The **multi-threaded** implementation performs roughly the same total number of operations as the single-process version. This clearly demonstrates the GIL in action: only one thread can execute Python bytecode at a time, so adding threads to a CPU-bound task adds no speedup (and may even add slight overhead).

The **multi-process** implementation, however, performs approximately 4x the number of operations in the same timeframe. This is expected, as it utilizes 4 fully independent processes running in parallel on different cores.

## Python's elephant in the room

The efficiency principles discussed so far apply to most programming languages. However, high-level languages like Python and R present a unique paradox that must be addressed.

Consider these two conflicting facts:

1. **Python is slow:** Benchmarks consistently rank it behind compiled languages.
2. **Python is the top language for Data Science:** It is the industry standard for computationally intensive fields.

Why is a "slow" language the preferred tool for high-performance data science?
The answer is simple: **It isn't.**

Python is not chosen because the heavy lifting is done *in* Python. It is chosen because it offers the best interface for **orchestrating** heavy lifting. Libraries like `pandas` (and `numpy`), `scipy`, `scikit-learn`, `pytorch`, and `tensorflow` are essentially wrappers. They provide a user-friendly Python layer that sits on top of highly optimized code written in C, C++, or Fortran.

Therefore, a "Python" data science project is often just a control layer; the actual computation happens in compiled languages.

This leads to a critical realization for efficient Python programming: when you use Python to orchestrate workloads, you are managing a complex system where a Python process triggers external compiled code.

We can observe this behavior by monitoring CPU load during a simple NumPy operation:

```python
import numpy as np

size = 4000
arr1 = np.random.rand(size, size)
arr2 = np.random.rand(size, size)
for _ in range(100):
    # simply perform the dot product of the two arrays
    np.dot(arr1, arr2)

```

On a Unix system, `btop` reveals the underlying activity:

Even though we ran a *single* Python process, all available cores are fully utilized.

Here is what happens:
NumPy utilizes `BLAS`, a highly optimized C library for linear algebra. Unlike Python, C code is not bound by the GIL. When Python calls the NumPy `dot` product, NumPy instructs the interpreter to release the GIL and pass control to the C library. The C code then spins up multiple threads to perform the calculation in parallel across all cores. Once finished, it returns control to Python, which re-acquires the GIL.

Attempting to manually parallelize this specific `for`-loop using Python threads or processes would likely be counterproductive. It would create a scenario where multiple processes fight for CPU resources that the BLAS library is already saturating, leading to context-switching overhead and reduced performance.

## Context switches in Python

There is another cost to using Python as a "facade" for compiled code: **Data Marshaling**.
Data must be translated from Python objects into C-compatible data structures. This translation consumes memory and CPU cycles. Performance bottlenecks in libraries like `numpy` or `pytorch` are frequently caused by inefficient management of this data transition.

To illustrate the cost of these context switches, consider the following benchmark:

```python
import numpy as np
import time

def timeit(func, iterations= 100, *args, **kwargs):
    """
    Measure overall duration of a repeated function call
    """
    start_time = time.perf_counter()
    for _ in range(iterations):
        func(*args, **kwargs)
    end_time = time.perf_counter()
    print(f"{iterations} calls of {func}:\t"
          f"{round(end_time - start_time, 3)} seconds")

def numpy_sum(np_array):
    """
    Use numpy's built in sum.
    """
    return np.sum(np_array)

def python_loop(collection):
    """
    Use conventinal python loop to sum an array or list.
    """
    python_sum = 0
    for num in collection:
        python_sum += num
    return python_sum

def python_sum(collection):
    """
    Use python built-in sum function
    """
    return sum(collection)

# Create a large NumPy array
np_array = np.random.rand(1000000)
# and a conventional python list
conventional_list = np_array.tolist()

print("NumPy array:")
# Calculate the sum using NumPy's built-in function
timeit(numpy_sum, 100, np_array)
# Calculate the sum using a Python sum
timeit(python_sum, 100, np_array)
# Calculate the sum using a Python loop over the NumPy array
timeit(python_loop, 100, np_array)
print("Python list:")
# Calculate the sum using a Python's sum
timeit(python_sum, 100, conventional_list)
# Calculate the sum using a Python loop over the conventional list
timeit(python_loop, 100, conventional_list)

```

A typical output demonstrates the disparity:

```
NumPy array:
100 calls of <function numpy_sum at 0x7fe9c1a29a80>:    0.041 seconds
100 calls of <function python_sum at 0x7fe97e443240>:   6.12 seconds
100 calls of <function python_loop at 0x7fe9c1a84cc0>:  6.926 seconds
Python list:
100 calls of <function python_sum at 0x7fe97e443240>:   0.748 seconds
100 calls of <function python_loop at 0x7fe9c1a84cc0>:  2.122 seconds

```

**Key Observations:**

1. **NumPy is fastest:** `numpy_sum` on a NumPy array is orders of magnitude faster because the loop happens entirely in C, with minimal Python interaction.
2. **Python loops are slow:** The `python_sum` on a standard list is roughly 20x slower than the pure NumPy version.
3. **The Marshaling Penalty:** The slowest performer is the Python loop iterating over a *NumPy array*. It is 100x slower than the NumPy implementation and even 3x slower than a standard Python list loop.

Why is the last case so slow? The `for`-loop forces the program to access individual elements of the NumPy array one by one. For every single number, the program must convert the data from a C type to a Python object to perform the addition. This constant conversion (marshaling) creates massive overhead.

While this example is simple, identifying such transition bottlenecks in complex, real-world applications can be much more difficult.

## Further resources

For advanced parallel and distributed computing in Python, the following 3rd party libraries are industry standards:

* [dask](https://docs.dask.org/en/stable/index.html)
* [joblib](https://joblib.readthedocs.io/en/stable/)
* [pyspark](https://spark.apache.org/docs/latest/api/python/index.html)

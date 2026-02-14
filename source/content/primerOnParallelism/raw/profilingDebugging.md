# Profiling and Debugging

In the landscape of complex software development, having a solid strategy to identify and resolve issues is non-negotiable.
Profiling and debugging are the twin pillars of this process, essential for elevating both code quality and runtime performance.

## Debugging

Bugs generally fall into two categories:

| Nice Bugs | Nasty Bugs |
| --- | --- |
|  |  |
| These bugs cause immediate failure, producing a clear traceback that usually points directly to the root cause. | These bugs lurk silently in your code, producing unexpected outputs or causing errors in downstream components long after the initial failure. |

If you encounter a **nice bug**, the hard work is often already done for you; the system has crashed and provided a traceback.
Mastering the art of reading these tracebacks is the fastest way to fix your code.
If you are unfamiliar with interpreting these error logs, the [Real Python Tutorial on Tracebacks](https://realpython.com/python-traceback/) is an excellent guide.

If, however, you suspect a **nasty bug**—where the code runs but the behavior is wrong—you should proceed with a structured debugging approach:

1. **Identify the bug**: First, confirm that the behavior is genuinely unexpected.
It is possible the code is correct, but the input data has changed or has unknown characteristics.
If you are unsure, try to reproduce the unexpected behavior consistently with different data sets.
2. **Reproduce the bug**: Isolate the issue. Ideally, write a unit test that consistently triggers the bug.
At the very least, create a minimal code snippet that replicates the issue.
If you are struggling to define the bug, try to establish "reference cases"—inputs where the output is known and correct—to contrast with the failure.
3. **Locate the source**: Pinpoint exactly where the logic diverges.
This requires inspecting the state of variables during execution.
While adding `print` statements is a common "quick and dirty" tactic, it is often messy.
A cleaner approach is to use a [`logger`](https://www.google.com/search?q=%5Bhttps://docs.python.org/3/library/logging.html%5D(https://docs.python.org/3/library/logging.html)) configured for debugging.
The most powerful method is using an interactive debugger, such as [ipdb](https://github.com/gotcha/ipdb). This allows you to pause execution at breakpoints, explore variable states, and even test code fixes interactively.
4. **Fix and Verify**: Apply the fix and confirm the issue is resolved without introducing regressions.

## Debuggers

Most modern IDEs feature integrated debugging tools that make it easy to set breakpoints, inspect variables, and step through code.
Alternatively, you can use powerful command-line debuggers that can be imported directly into your script.
We recommend `ipdb` as a robust tool for interactive debugging.
To use it, simply insert the following line at the point where you want to inspect your code:

```python
import ipdb; ipdb.set_trace()  # BREAKPOINT

```

Then, run your Python script in your shell as usual. The execution will pause at this line, dropping you into an interactive prompt.

## Profiling

Profiling tools are vital for diagnosing performance bottlenecks and analyzing memory usage. They tell you exactly where your application is spending its time.

Here are some standard tools and approaches:

* **Ad-hoc Timing:** Use Python’s built-in `time.perf_counter_ns()` for quick, specific measurements of code blocks.
* **Deterministic Profiling:** The standard [Profile](https://docs.python.org/3/library/profile.html#module-cProfile) module is the go-to choice for comprehensive performance statistics.
* **Line-by-Line Analysis:** The [line_profiler](https://github.com/pyutils/line_profiler) package offers granular statistics for every line of code in a function.
* **Memory Profiling:** [memray](https://bloomberg.github.io/memray/) is a high-performance, 3rd-party tool that provides detailed insights into memory allocation.
* **Ecosystem:** Many other specialized tools exist; select the one that best fits your specific bottleneck (CPU vs. Memory).

For projects with automated testing, integrating profiling into CI/CD pipelines is highly recommended. For instance, the `memray pytest` plugin allows you to capture memory profiles during unit tests, ensuring that performance regressions are detected immediately.

We strongly encourage you to experiment with tools like `line_profiler` and `memray`. Understanding where your code is slow or memory-hungry is the first step toward writing efficient, professional-grade software.

## Additional Hints

* **Isolate Profiling:** Avoid performing memory and timing profiling in the same run, as the overhead from one can distort the results of the other.
* **Logging vs. Print:** Use logging or warnings for diagnostic output rather than simple print statements.
Consult the Python logging module documentation to learn best practices for structured application logging.

## Further resources

* [Real Python's tutorial on tracebacks](https://realpython.com/python-traceback/)
* [GeeksForKees's tutorial for ipdb](https://www.geeksforgeeks.org/using-ipdb-to-debug-python-code/)
* [python logging module](https://docs.python.org/3/library/logging.html)

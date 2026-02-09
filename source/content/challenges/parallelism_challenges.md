{% if build == "slides" %}
# Task Multiplicity & Parallelism
{% else %}
## Managing Multiple Tasks and Parallel Execution
{% endif %}

{% if slide %}
**Scientific computing often involves many related tasks**

**Common patterns:**
- Running the same analysis on multiple datasets
- Parameter sweeps exploring different configurations
- Ensemble simulations with varied initial conditions
- Pipeline stages that can run independently

**Why this is challenging:**
- Manual execution doesn't scale
- Dependencies between tasks require coordination
- Resource allocation needs optimization
{% endif %}

:::{admonition} Ensemble Learning
:class: margin
**Bagging**: Bootstrap Aggregation reduces variance by training models in parallel on random subsets (e.g., Random Forest).

**Boosting**: reduces bias by sequentially training models with increased weights of misclassified data points in subsequent models (AdaBoost, XGBoost, Gradient Boosting, etc.).
:::

{% if page %}
Scientific computing frequently involves not just one computation, but many related computations. This task multiplicity arises naturally from the scientific method: testing multiple hypotheses, exploring parameter spaces, validating across different datasets, or running ensemble simulations.

### Sources of Task Multiplicity

Task multiplicity appears in several forms:

- **Batch processing**: Applying the same analysis to many different input files or datasets
- **Parameter sweeps**: Exploring how results vary across different parameter combinations
- **Ensemble methods**: Running multiple simulations with varied initial conditions or parameters to assess variability
- **Pipeline stages**: Multi-step workflows where different stages can potentially run simultaneously

Manual execution of multiple tasks quickly becomes impractical. Managing dozens or hundreds of related computations by hand is error-prone and inefficient.
{% endif %}

{% if build == "slides" %}
---
{% else %}
### Enabling and Exploiting Parallelism
{% endif %}

{% if slide %}
**Parallelism can dramatically reduce wall-clock time**

:::::{grid} 2
::::{grid-item-card} The Opportunity
- Multiple CPU cores sit idle if not used
- Many tasks are independent and can run simultaneously
- Potential for significant speedups
::::

::::{grid-item-card} The Challenges
- Code must be written to support parallelism
- Data access patterns must avoid conflicts
- Synchronization and communication add overhead
::::
:::::

:::{admonition} Not All Parallelism Is Equal
:class: note
- **Embarrassingly parallel**: Independent tasks (easiest)
- **Shared memory**: Threads within one machine (moderate complexity)  
- **Distributed**: Across multiple machines (most complex)
:::
{% endif %}

{% if page %}
Modern computing systems provide substantial parallel capacity through multiple CPU cores, multiple machines, and specialized architectures. However, exploiting this capacity requires that code and algorithms are designed for parallelism.

### Why Parallelism Is Challenging

Several factors complicate parallel execution:

**1. Algorithm structure**: Not all algorithms can be parallelized. Some computations are inherently sequential, where each step depends on the previous one.

**2. Code architecture**: Programs written for sequential execution often need significant restructuring to work in parallel. This includes managing how data is shared or distributed across parallel workers.

**3. Overhead costs**: Parallel execution introduces overhead from:
   - Splitting work across workers
   - Communication between workers
   - Synchronization to ensure consistency
   - Load balancing to keep all workers busy

**4. Diminishing returns**: Amdahl's Law states that if a program has any sequential component, there's a limit to speedup from parallelization. This fundamental principle quantifies the theoretical speedup limit when parallelizing a program. If a fraction *s* of the program must run sequentially, the maximum speedup with *N* processors is 1/(s + (1-s)/N). For example, if 10% of your code is sequential, the maximum speedup is 10×, no matter how many processors you add. This law emphasizes the critical importance of minimizing sequential bottlenecks.

![Amdahl's Law visualization showing speedup versus number of processors for different percentages of parallelizable code](https://upload.wikimedia.org/wikipedia/commons/e/ea/AmdahlsLaw.svg)

*Theoretical speedup according to Amdahl's Law for different proportions of parallelizable code. Even small sequential portions significantly limit maximum speedup.*

### Types of Parallelism

Different types of parallelism have different complexity levels:

- **Embarrassingly parallel**: Tasks that are completely independent. These are the easiest to parallelize and scale well.
- **Shared memory parallelism**: Multiple threads working on the same data within one machine. Requires careful synchronization to avoid conflicts.
- **Distributed parallelism**: Computation across multiple machines. Requires handling network communication and potential failures.

Each level introduces more complexity but potentially enables larger-scale computation.
{% endif %}

{% if build == "slides" %}
---
{% else %}
### Data and Workflow Management in Parallel Environments
{% endif %}

{% if slide %}
**Parallelism creates data management complexity**

**Key challenges:**
- **Race conditions**: Multiple processes trying to write the same file
- **Data consistency**: Ensuring all workers see the same data state
- **Output organization**: Collecting and organizing results from many parallel tasks
- **Intermediate data**: Where to store temporary results from parallel stages

**Workflow orchestration:**
- Task dependencies require careful scheduling
- Failures in parallel tasks need detection and handling
- Resource allocation must balance parallelism with available capacity
{% endif %}

{% if page %}
Parallel execution introduces significant data management challenges that don't exist in sequential computation.

### Race Conditions and Conflicts

When multiple processes run simultaneously, conflicts can occur:

- **Write conflicts**: Two processes attempting to write the same file simultaneously can corrupt data
- **Read-write conflicts**: One process reading while another writes can see incomplete or inconsistent data
- **Resource contention**: Multiple processes competing for the same resource (network bandwidth, disk I/O) can cause performance degradation

These require explicit coordination mechanisms: file locking, atomic operations, or architectural patterns that avoid conflicts (e.g., each process writes to its own output file).

### Output Management

Organizing results from parallel execution requires planning:

- **Naming conventions**: Each parallel task needs distinct output files or a system to merge results
- **Aggregation**: Combining results from many parallel tasks into final results
- **Partial results**: Handling incomplete results if some parallel tasks fail
- **Data provenance**: Tracking which outputs came from which inputs and parameters

### Workflow Orchestration

Complex workflows with dependencies between tasks require orchestration:

- **Task scheduling**: Ensuring tasks run in the correct order when there are dependencies
- **Resource management**: Allocating CPU, memory, and other resources across parallel tasks without oversubscription
- **Failure handling**: Detecting when parallel tasks fail and deciding whether to retry, skip, or abort
- **Progress tracking**: Monitoring which tasks have completed and which are still running

These challenges necessitate workflow management tools and careful system design to handle the complexity of parallel execution reliably.
{% endif %}

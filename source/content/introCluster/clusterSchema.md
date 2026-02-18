## HPC Cluster Schema

{% if page %}

Hardware aggregation done with high-speed networking leads to a system with the well-known name of High Performance Computing (HPC) Cluster.

{% endif %}

```{figure} ./../_static/slurmCluster.png
:alt: Slurm Cluster
:width: 100%
```

{% if page %}

An HPC Cluster is more than just a powerful server; it is a unified, software-orchestrated fleet of computers.
An HPC Cluster is essentially a collection of distinct physical machines that simulate the anatomy of a single supercomputer.

First, the Cluster relies on the **Login Nodes** (or Head Nodes), which act as the system’s gateway.  
These specific servers serve as the users "control room", specifying where job submissions, script editing, and software environment management occur.
These nodes can be comparet to the terminal on a local laptop, but with one critical rule: they are for orchestration, not calculation!
Login Nodes are the interface where resource definitions are made, such as the number of GPUs, the amount of RAM, or the wall-time for a training run.

Second, the Cluster possesses a **Workload Manager** (or Scheduler).  
Just like a project manager assigning tasks to a team, this critical piece of software (often Slurm or PBS) acts as the broker between the code and the hardware.
It reads the "job scripts" — the blueprints declaring requirements — and places the task into a queue.
It waits until the specific combination of requested resources becomes available before dispatching the job to the hardware.

Third, the Cluster is built on **Compute Nodes**, which act as the system's processing power.  
These are often multiple racks of distinct, powerful servers — the digital equivalent of the CPU and GPU in a workstation, but scaled up significantly.
This is where the calculation actually happens; when the scheduler dispatches a job, the Python or R code executes on the specific CPUs or GPUs of these distinct machines.

Finally, there is the **Shared Storage**, which is the digital equivalent of the physical hard drive found in a standard computer.  
This persistent storage container (parallel file systems like Lustre or GPFS) holds massive datasets, trained models, and simulation results.
Because this storage is mounted on every node, a model trained on a Compute Node is immediately visible and accessible on the Login Node for analysis.

**The defining characteristic of this system is the Interconnect.**
The individual Compute Nodes operate under the illusion that they are close neighbors.
In reality, high-speed cables (like InfiniBand) link these separate machines, allowing them to pass data back and forth with such low latency that they can function as a single, coherent unit for distributed training or massive data processing.

{% endif %}


(slurm)=
# Slurm

An open source cluster controller and allocation manager providing a framework for starting, executing and monitoring work.

{% if slide %}:::{card}{% else %}##{% endif %} <i class="fas fa-sitemap"></i> Anatomy of a Slurm cluster
- **Login Node**: The "Doorway". Edit files, compile code, submit jobs.
- **Controller**: The "Bouncer". Allocates resources ([Slurm](#slurm), PBS).
- **Compute Nodes**: The "Workers". Where the actual calculation happens.
- **Storage**: Shared filesystem (Global `HOME`, `SCRATCH`).
{% if slide %}:::{% endif %}

## Architecture

Resource management done with a centralized controller leads to a system structure known as the Slurm Workload Manager.
Slurm is more than just a job scheduler; it is a modular, fault-tolerant operating system for the cluster.
It is essentially a collection of distinct daemons and tools that simulate a single, unified computing entity.

```{figure} ./../_static/slurmArchitecture.png
:alt: Slurm Architecture
:width: 100%
```

First, the system relies on the Centralized Manager (slurmctld), which acts as the system’s brain.
This daemon monitors resources and work, maintaining the state of the entire cluster in memory.
To ensure continuous operation, a backup manager may also exist to assume these responsibilities in the event of a primary failure.
There is also an optional REST API Daemon (slurmrestd), which allows for interaction with Slurm through standard web-based APIs.

Second, the Cluster possesses the Node Daemon (slurmd).
Residing on each compute server (node), this daemon functions comparably to a remote shell: it waits for work, executes that work, returns status, and waits for more work.
These daemons provide fault-tolerant hierarchical communications, ensuring that the instructions from the controller are reliably executed on the hardware.

Third, there is the Database Daemon (slurmdbd), which acts as the system's long-term memory.
This optional component records accounting information for multiple Slurm-managed clusters in a single database.
Managed by the administrative tool sacctmgr, it identifies the clusters, valid users, and valid accounts, enforcing limits and tracking usage over time.

Finally, there are the User and Administrative Tools, which act as the interface.
User tools include srun to initiate jobs, scancel to terminate queued or running jobs, sinfo to report system status, and squeue to report the status of jobs.
For historical analysis, sacct provides information about jobs and job steps that are running or have completed.
Administrators utilize scontrol to monitor and modify configuration and state information on the cluster, while sview offers a graphical report of system and job status, including network topology.


{.samller}
**Sources**:   
<https://slurm.schedmd.com/>  

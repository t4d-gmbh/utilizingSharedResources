## Slurm Cluster Architecture


[Slurm](#slurm) is essentially a collection of distinct daemons and tools that simulate a single, unified computing entity.


```{figure} ./../_static/slurmArchitecture.png
:alt: Slurm Architecture
:width: 100%
```
{% if page %}

The **Core Architecture** (Orchestration):  
The system relies on a Centralized Manager (slurmctld), which acts as the system’s brain.
This daemon monitors resources and work, maintaining the state of the entire cluster in memory.
To ensure continuous operation, a backup manager may also exist to assume these responsibilities in the event of a primary failure.
Interfaces are modernized through the optional REST API Daemon (slurmrestd), which allows for interaction with Slurm through standard web-based APIs.

The **Compute Fabric** (Execution):  
The Cluster possesses the Node Daemon (slurmd) residing on each compute server.
This daemon functions comparably to a remote shell: it waits for work, executes that work, returns status, and waits for more work.
These daemons provide fault-tolerant hierarchical communications, ensuring that instructions from the controller are reliably executed on the hardware.

The **Accounting** (Data Persistence):  
There is the Database Daemon (slurmdbd), which acts as the system's long-term memory.
This optional component records accounting information for multiple Slurm-managed clusters in a single database.
It is managed by the administrative tool sacctmgr, which identifies valid users, accounts, and clusters, enforcing limits and tracking usage over time.

The **Interface** (User & Admin):  
User tools include srun to initiate jobs, scancel to terminate queued or running jobs, sinfo to report system status, and squeue to report the status of jobs.
For historical analysis, sacct provides information about jobs and job steps that are running or have completed.
Administrators utilize scontrol to monitor and modify configuration and state information on the cluster, while sview offers a graphical report of system and job status, including network topology.


{% endif %}

(slurm)=
# Slurm

An open source cluster controller and allocation manager providing a framework for starting, executing and monitoring work.

:::{image} ./static/slurmCluster.png
:align: center
:height: 350px
:alt: Cloud Operating System Architecture
:::
{% if slide %}:::{card}{% else %}##{% endif %} <i class="fas fa-sitemap"></i> Anatomy of a Slurm cluster
- **Login Node**: The "Doorway". Edit files, compile code, submit jobs.
- **Controller**: The "Bouncer". Allocates resources ([Slurm](#slurm), PBS).
- **Compute Nodes**: The "Workers". Where the actual calculation happens.
- **Storage**: Shared filesystem (Global `HOME`, `SCRATCH`).
{% if slide %}:::{% endif %}

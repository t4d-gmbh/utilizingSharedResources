# <i class="fa-solid fa-sitemap"></i> HPC Clusters

```{admonition} [Clusters](#cluster)
:class: tip, margin

Computer clusters can have various functionalities, HPC is just one of them.
```
High Performance Computing as a Service (HPCaaS) deployments are commonly called: HPC Clusters

{% if slide %}
<!-- BUILDING THE SLIDES -->
```{toctree}
:maxdepth: 3

./clusterSchema
./clusterFeatures
./clusterArchitecture

```

{% else %}
<!-- BUILDING THE PAGES -->

```{include} ./clusterSchema.md
```
```{include} ./clusterFeatures.md
```
```{include} ./clusterArchitecture.md
```

{.smaller}
**Sources**:  
<https://en.wikipedia.org/wiki/High-performance_computing>  
<https://en.wikipedia.org/wiki/Computer_cluster>  
<https://slurm.schedmd.com>  
{% endif %}


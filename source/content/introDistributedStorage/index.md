# Distributed Storage

{% if slide %}
<!-- BUILDING THE SLIDES -->
```{toctree}
:maxdepth: 3

./sharedStorageTypes
./blockStorage
./objectStorage
./sharedFilesystem
```

{% else %}
<!-- BUILDING THE PAGES -->

```{include} ./sharedStorageTypes.md
```
```{include} ./blockStorage.md
```
```{include} ./objectStorage.md
```
```{include} ./sharedFilesystem.md
```
{.smaller}
**Sources**:  
<https://docs.ceph.com/en/>   
<https://docs.openstack.org/>  
<https://slurm.schedmd.com/documentation.html>  
<https://wiki.lustre.org/Main_Page>  
{% endif %}

{% if slide %}
{% else %}
{% endif %}


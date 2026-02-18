# The <i class="fa-solid fa-cloud"></i> Cloud

Infrastructure as a Service (IaaS) products are often simply called: Clouds

{% if slide %}
<!-- BUILDING THE SLIDES -->
```{toctree}
:maxdepth: 3

./virtualization
./vm
./container
./theCloudSchema
./cloudFeatures
./cloudOS
```

{% else %}
<!-- BUILDING THE PAGES -->

```{include} ./virtualization.md
```
```{include} ./vm.md
```
```{include} ./container.md
```
```{include} ./theCloudSchema.md
```
```{include} ./cloudFeatures.md
```
```{include} ./cloudOS.md
```

{.smaller}
**Sources**:  
<https://en.wikipedia.org/wiki/Virtualization>  
<https://en.wikipedia.org/wiki/Hardware_virtualization>  
<https://en.wikipedia.org/wiki/Hypervisor>  
<https://docs.openstack.org/2025.2>  
{% endif %}


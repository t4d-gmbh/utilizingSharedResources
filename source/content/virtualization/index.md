# Virtualization

Virtualization is the technology that allows multiple independent computing environments to run on shared physical hardware, enabling the flexible and efficient resource utilization that underpins modern scientific computing infrastructure.

{% if slide %}
<!-- BUILDING THE SLIDES -->
```{toctree}
:maxdepth: 3

./virtualization
./vm
./container
```

{% else %}
<!-- BUILDING THE PAGES -->

```{include} ./virtualization.md
```
```{include} ./vm.md
```
```{include} ./container.md
```

{.smaller}
**Sources**:  
<https://en.wikipedia.org/wiki/Virtualization>  
<https://en.wikipedia.org/wiki/Hardware_virtualization>  
{% endif %}


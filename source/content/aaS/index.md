# <i class="fa-regular fa-star"></i> as a Service


{% if slide %}
<!-- BUILDING THE SLIDES -->
```{toctree}
:maxdepth: 3

./youKnow
./usage
./IaaS
./HPCaaS
./STaaS
```

{% else %}
<!-- BUILDING THE PAGES -->

```{include} ./usage.md
```
```{include} ./IaaS.md
```
```{include} ./HPCaaS.md
```
```{include} ./STaaS.md
```

{.smaller}
**Sources:**  
<https://en.wikipedia.org/wiki/As_a_service>  
<https://en.wikipedia.org/wiki/Infrastructure_as_a_service>  
<https://en.wikipedia.org/wiki/High-performance_computing>  
<https://en.wikipedia.org/wiki/Software-as-a-service>  
<https://www.ibm.com/think/topics/storage-as-a-service>
{% endif %}

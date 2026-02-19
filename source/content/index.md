```{toctree}
:maxdepth: {% if build == "slides" %}1{% else %}2{% endif %}
:caption: Utilizing Shared Resources

{% if build == "slides" %}yourChallenges/index
{% endif %}challenges/index
introComputerChips/index
fromMhzToTeraflops/index
concurrency/index
primerOnParallelism/index
fromConcurrencyToService/index
aaS/index
resourceSharingPrinciple/index
introCloud/index
introCluster/index
introDistributedStorage/index
suitabilityChecklist/index
{% if page %}terminology/index{% endif %}

```

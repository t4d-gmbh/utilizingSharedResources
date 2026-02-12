# Shared Resources

{% if build == "slides" %}
```{toctree}
:maxdepth: 3

./multiTenancy
./virtualization
```

{% else %}



```{include} ./multiTenancy.md
```
```{include} ./virtualization.md
```

{% endif %}


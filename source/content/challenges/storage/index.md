{% if build == "slides" %}
# Storage Challenges

```{toctree}

./intro
./quotas
./data_movement
./large_datasets
```

{% else %}

# Storage Challenges

```{include} ./intro.md
```

```{include} ./quotas.md
```

```{include} ./data_movement.md
```

```{include} ./large_datasets.md
```

{% endif %}

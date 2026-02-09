{% if build == "slides" %}
# Challenges in Computational Projects

```{toctree}
:maxdepth: 1
:numbered:

./intro
./storage_challenges
./compute_challenges
./parallelism_challenges
./reproducibility_challenges
```

{% else %}

# Challenges in Computational Projects

This section introduces the practical challenges when working on computational projects. 
Understanding these challenges provides context for the tools and approaches covered in this course.

```{include} ./intro.md
```

```{include} ./storage_challenges.md
```

```{include} ./compute_challenges.md
```

```{include} ./parallelism_challenges.md
```

```{include} ./reproducibility_challenges.md
```

{% endif %}

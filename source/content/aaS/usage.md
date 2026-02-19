---
sd_hide_title: true
---
## Usage & Origins


```{figure} ../_static/everythingaaS.png
---
figclass: margin-caption
alt: My figure text
name: everythingaaS
{% if page %}
width: 100%
figclass: margin
{% else %}
width: 60%
{% endif %}
---
```
{% if slide %}

::::{grid} 1 1 2 2
:gutter: 3

:::{grid-item-card} **<i class="fa-regular fa-star"></i> as a Service**
:class: sd-m-auto
Broadly applied to subscription models.  
Wikipedia lists **over 35 business models**.

*Finds application well outside IT (e.g. Transport aaS)*

{.smaller} 
<https://en.wikipedia.org/wiki/As_a_service>
:::

:::{grid-item-card} Scientific Context
- Infrastructure as a Service (**IaaS**)
- High Performance Computing as a Service (**HPCaaS**)
- Storage as a Service (**STaaS**)
:::

::::

{% else %}

The phrasal template arguably originated from the concept of Software as a Service (SaaS) and has since been broadly applied to subscription-based business models.
As of February 2026, the template's own Wikipedia page[^1] lists over 35 distinct business models using this nomenclature.

In a scientific context, especially in computational sciences, this paradigm has considerably altered research infrastructure.
It shifts the heavy burden of managing physical hardwar like power, cooling, maintenance, and networking, from the scientist to specialized providers.
This allows researchers to treat computing power not as a piece of equipment they must buy and repair, but as a flexible utility they consume.
Consequently, scientists can focus on their specific domain questions rather than the intricacies of IT administration.

[^1]: <https://en.wikipedia.org/wiki/As_a_service>

{% endif %}

{% if build == "slides" %}
## Storage Quotas and Legal Constraints
{% else %}
### Storage Quotas and Legal Constraints
{% endif %}

{% if slide %}
**Why do storage quotas exist?**

- Finite physical resources must be shared fairly
- Legal requirements restrict data location and handling
- Costs scale non-linearly with capacity and performance

{% endif %}

{% if page %}
Storage quotas aren't arbitrary restrictions, they reflect real operational constraints. Shared computing facilities must allocate resources equitably across many users and projects. Unrestricted storage by one project would disadvantage others.

Legal and regulatory requirements add complexity. Certain types of data (personal information, sensitive research data) may have restrictions on where and how they can be stored. This can limit storage options even when resources are available.

These constraints mean researchers must make strategic decisions about what to store, when to store it, and when to regenerate data instead.
{% endif %}

{% if slide %}

---

**Quota Impact**

Strategic decisions are required:
- Cannot store unlimited intermediate results
- May need to regenerate data rather than cache it
- Data locality becomes strategically important

{% endif %}

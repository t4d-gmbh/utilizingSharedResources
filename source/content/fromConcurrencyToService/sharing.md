## Resource sharing

:::{figure} ./../_static/share.png
:alt: laws
:width: 100%
{% if page %}:figclass: margin{% endif %}
:::

{% if page %}

Multitenancy enables a single underlying infrastructure to serve multiple distinct users (tenants) simultaneously.
In modern infrastructures this is sometimes achieved through a Multi-instance architecture, where the concurrent capabilities of the hardware are used to spawn isolated environments (or instances) for each tenant.
While the physical resources (CPU, RAM, Storage) are shared at the lowest level, each tenant interacts with their own private instance, unaware of the others.

By pooling the workloads of diverse users onto a single shared infrastructure, the system can leverage concurrency to fill the 'idle gaps' left by one user with the active tasks of another.

In this model, the intense but intermittent demands of multiple tenants are interleaved. When one tenant pauses (e.g., waiting for data), the system instantly switches context to process another tenant's request. This ensures that the expensive, high-performance components, such as the CPU, cache, and specialized accelerators, are kept in near-constant use.

Consequently, multitenancy transforms the risk of hardware complexity into an economic advantage: the immense cost of a powerful, specialized computer is no longer a burden for a single user, but is amortized across many, making high-performance computing accessible and affordable for all.

Fundamentally, multitenancy transforms physical hardware into a shareable resource that can be provided as a service to others. Instead of every user requiring their own isolated machine, the system becomes a communal pool of computing power, partitioned logically rather than physically.

In an abstract sense, the rise of the Internet (originating with ARPANET in the late 1960s and standardized in the early 1980s) was the pivotal technology that unlocked this potential on a global scale. While early time-sharing systems allowed users to share a mainframe within a single building, the Internet acted as a conduit that allowed computing resources to be shared over vast distances. It decoupled the user of the computation from the location of the hardware, effectively turning processing power into a utility that could be delivered through a wire.


{% endif %}

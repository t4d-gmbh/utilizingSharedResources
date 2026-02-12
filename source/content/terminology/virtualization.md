(virtualization)=
## Virtualization

{% if slide %}
:::::{grid} 2
::::{grid-item-card} <i class="fas fa-layer-group"></i> The Concept
- **Abstraction**: Decoupling software from hardware.
- **Partitioning**: Running multiple OSes on one physical machine.
- **Isolation**: Fault and security containment.
::::

::::{grid-item-card} <i class="fas fa-microchip"></i> The Parts
- **Cloud Operating System**: Orchestrator pooling resources across multiple hosts.
- **Hypervisor**: The software layer creating VMs.
- **Guest**: The virtualized system.
- **Host**: The underlying physical hardware.
::::
:::::
{% else %}

Virtualization is the process of creating a virtual (rather than actual) version of computer infrastructure.
This can include virtual computer hardware platforms, storage devices, and computer network resources.

{% endif %}

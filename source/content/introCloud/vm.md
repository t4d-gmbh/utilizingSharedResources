### Virtual Machine (VM)

{% if slide %}
```{epigraph}
{.centered}
The product of hardware virtualization.
```

{% else %}

Hardware virtualization done with any type of Hypervisor leads to a product with the well known name of Virtual Machine (VM).

{% endif %}

::::{grid}
:gutter: 3

:::{grid-item}
:column: 6
:class: sd-m-auto

{% if slide %}

**Hardware Definition**:  
Configuration file declaring the "Hardware".

**Virtual Firmware**:  
Minimal piece software to initialize the hardware for the bootloader.

**Disk Image**:  
Single file that acts as the "hard drive".

{% else %}

A Virtual Machine (VM) is more than just a Guest OS; it is a complete, software-defined computer.
A VM is essentially a collection of distinct components that simulate the anatomy of a physical machine.


{% endif %}

:::
:::{grid-item}
:columns: 6
:class: sd-m-auto

```{image} ../_static/vm.png
:alt: VM
:name: VM
:width: 100%
```
:::

::::

{% if page %}

First, the VM relies on a **Hardware Definition**, which acts as the system's blueprint.
This configuration file (often XML in KVM/OpenStack) declares the virtual "motherboard," specifying exact resources such as the number of vCPUs, the amount of RAM, and specific network or graphics cards.
The Hypervisor reads this blueprint to wire together the virtual circuits.

Second, the VM possesses **Virtual Firmware** (BIOS or UEFI).
Just like a physical server or computer, this tiny piece of software initializes the hardware when the "Power On" signal is sent, performing the critical boot sequence before the Operating System ever loads.

Finally, there is the **Disk Image**, which is the digital equivalent of the physical hardware storage you interact with daily.
You can think of this file (formats like `.qcow2` or `.vmdk`) exactly like the physical **Solid State Drive (SSD) or Hard Drive inside your laptop**.
It is the persistent storage container that holds the Guest OS, the bootloader, and all your personal data.

The defining characteristic of this system is **Hardware Emulation**.
The Guest OS operates under the illusion that it is interacting with real, physical hardware components.
In reality, the Hypervisor intercepts these instructions—such as writing a file to the "disk"—and translates them into valid calls for the underlying Host Operating System.

{% endif %}

### Container

{% if slide %}
```{epigraph}
{.centered}
The product (one of many) of OS-level virtualization.
```
{% else %}

Virtualization at the OS level leads to various products, like Zones, Jails, Virtual Private Servers, but most notably: Containers.

{% endif %}

::::{grid}
:gutter: 3

:::{grid-item}
:columns: 6
:class: sd-m-auto

```{image} ../_static/container.png
:alt: Container
:name: Container
:width: 100%
```
:::
:::{grid-item}
:column: 6
:class: sd-m-auto

{% if slide %}


**Container Image**:  
Layered image of a filesystem. Single layers can be replaced.

**Manifest**:  
Declaring resource access and what to run.  

**Isolation Mechanism**:
Isolates the container process from the rest of the OS with Namespaces and Control Groups.

```{admonition} Analogy: Shared Lab Space
* **Namespaces**: Each researcher sees only their own bench and experiments
* **Cgroups**: Each gets allocated compute hours, storage quota, equipment time
```


{% else %}

A container is not merely a running user space or an isolated process; it is a portable packaging format combined with strict kernel containment rules.
It consists of three essential components: the **Image**, the **Manifest**, and the **Isolation Mechanisms**.


:::
::::

{% if page %}

#### The Image: A Layered Filesystem  
A container starts as a static file known as the **Image**.
Unlike a Virtual Machine, which is a single, monolithic file containing an entire operating system, a container image is built using a unique **Layered Approach**.

In this model, the filesystem is constructed by stacking multiple read-only changes on top of one another.
When the container engine reads the image, it uses a Union Filesystem to merge these separate layers into a single, cohesive view.

**Example of a Layered Image**:
When deploying a Python web application the image would be built in the following stack:

* Layer 1 (The Base):  
This contains the minimal Operating System files (e.g., Alpine Linux or Ubuntu Minimal).
This layer is read-only.

* Layer 2 (The Runtime):  
Installation of Python on top of the base.
This layer records *only* the difference (the new Python binaries) added to Layer 1.

* Layer 3 (The Application):  
Copy the source code (e.g., `app.py`) into a folder.
This records only the added code files.

* Layer 4 (The Container Layer):  
This is the **Read-Write layer**.
When the container starts, this thin, ephemeral layer is added on top.
Any file the application creates or modifies (like logs or temp files) is written here.

**Why Layering Matters:**
This approach provides massive efficiency.
Different applications that all use Python on Alpine Linux all **share** the exact same physical copy of Layer 1 and Layer 2 on the disk.
The system only stores the differences (Layer 3) for each app.
A VM, by contrast, would require ten full copies of the OS and Python, wasting gigabytes of space.

#### The Manifest (The Config)
Accompanying the image is the Manifest, a text file (typically JSON) that acts as the instruction manual for the container engine.
It describes exactly how to run the image.
It contains instructions such as: "Run the command `python app.py` on startup," "Expose network port 80," or "Mount the local folder `/data` into the container."

#### The Isolation Mechanisms (The Walls)
When the container actually starts, the engine (such as Docker or Podman) does not "boot" an OS in the traditional sense.
Instead, it instructs the existing Linux Host Kernel to erect invisible walls around the application process.
This is achieved using two specific kernel features:

**Namespaces (Visibility):**  
These limit what the process can *see*.
For example, a PID Namespace ensures the container sees its own process as "PID 1" and cannot see or interact with other processes running on the host.

**Cgroups (Control Groups - Resources):**  
These limit what the process can *use*.
They allow the administrator to set strict limits, such as "This container may use a maximum of 50% of one CPU core and 512MB of RAM," ensuring no single container can exhaust the host's resources.

**A Practical Analogy: The Shared Research Lab**

To make namespaces and cgroups more concrete, imagine a university research lab where multiple students share a single physical space and computing infrastructure.

**Namespaces as Isolation Walls:**  
Each student works at their own bench with their own experiments.
When Student A logs into the shared compute server, they see only their own running processes and files in their home directory.
They cannot accidentally delete Student B's data or interfere with Student C's long-running simulation.
This is what namespaces provide: each container believes it is the only tenant on the system, seeing only its own "PID 1" process and its own filesystem tree, even though dozens of other containers might be running simultaneously on the same kernel.

**Cgroups as Resource Quotas:**  
The lab manager allocates resources fairly: Student A gets 100 hours of GPU time per month, 500GB of storage, and access to 8 CPU cores maximum.
Student B gets a different allocation based on their project needs.
Without these limits, one student running an inefficient script could monopolize all 64 cores, blocking everyone else's work.
Cgroups enforce these boundaries automatically.
If a container tries to use more than its allocated 512MB of RAM, the kernel either denies the request or terminates the container rather than allowing it to crash the entire host.

This two-layer approach is what makes containers both secure and efficient for multi-tenant environments like research clusters or cloud platforms.

{% endif %}

{% endif %}

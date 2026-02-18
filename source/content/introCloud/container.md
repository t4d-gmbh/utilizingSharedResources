### Container

{% if slide %}
```{epigraph}
{.centered}
The product (one of many) of OS-level virtualization.
```
{% else %}

Virtualization at the OS level leads to various products, like Zones, Jails, Virtual Private Servers, but most notably: Containers.

{% endif %}

```{admonition} [Dockerfile](#Dockerfile)
:class: tip, margin
The `dockerfile` can contain both instructions for the image and the manifest!
```

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

{% else %}

A container is not merely a running user space or an isolated process; it is a portable packaging format combined with strict kernel containment rules.
It consists of three essential components: the **Image**, the **Manifest**, and the **Isolation Mechanisms**.


:::
::::

{% if page %}

#### The Image: A Layered Filesystem  
A container starts as a static file known as the **Image**.
Unlike a Virtual Machine disk, which is a single, monolithic file containing an entire Operating System, a container image is built using a unique **Layered Approach**.

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
{% endif %}

{% endif %}

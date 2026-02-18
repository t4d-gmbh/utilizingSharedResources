## Cloud Computing Schema

```{figure} ./../_static/cloudOS.png
:alt: powerWall
:width: 100%
```

{% if page %}

From a user perspective, a cloud environment provides two distinct interaction channels:

**The Management Channel (Control Plane)**:  
This interaction occurs via a Web Console (GUI), Command Line Interface (CLI), or SDK (API).
It is used to provision, configure, and monitor resources.
Crucially, this is also where bootstrapping occurs—allowing you to inject the necessary credentials (like SSH public keys or startup scripts) that enable the second channel.

**The Resource Channel (Data Plane)**:  
This is the direct interaction with the active workload.
While the Management GUI often provides a fallback "Console Access" (simulating a physical monitor via VNC), day-to-day operations are achieved through standard protocols like SSH (for Linux), RDP (for Windows), or application-level interfaces (e.g., HTTPS for JupyterLab).

The cloud operating system acts as orchestrator allocating the necessary resources to the users requests.
It manages the life-cycles of VMs including backups, snapshots and shelfing (store a switched of VM for later use).

{% endif %}

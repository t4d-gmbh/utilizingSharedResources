(dockerfile)=
## Dockerfile

A Dockerfile contains two completely different types of instructions: those that **build the filesystem layers** (the heavy lifting) and those that **update the metadata/manifest** (the instructions for the runtime).

Here is how the commands map to those two concepts:

**Layer Instructions**  

These commands actually change the files on the disk. Every time you run one of these, the builder takes a snapshot of the filesystem, calculates the difference (diff), and saves it as a new **Layer** (a compressed tarball).

* **`FROM ubuntu:20.04`**  Starts with the base layer.
* **`COPY . /app`**  Adds files from your laptop. Creates a new layer containing just those files.
* **`RUN apt-get install python`**  Runs a command, sees what files changed, and saves those changes as a new layer.

**Result:** These create the physical "blobs" that take up space (MB or GB) in your registry.

**Manifest/Metadata Instructions**:  

These commands **do not create layers** or add any file size. They simply update the **Image Configuration** (which ends up in the Manifest). They are notes passed to the container engine (like Kubernetes or Docker) on *how* to use the image.

* **`EXPOSE 80`**  Writes to the config: *"Whoever runs this, know that I intend to listen on port 80."* (It doesn't actually open the port; it just documents it).
* **`CMD ["python", "app.py"]`**  Writes to the config: *"If the user doesn't say otherwise, run this command when starting."*
* **`ENV APP_VERSION=1.0`**  Writes to the config: *"Set this variable in the process environment."*
* **`WORKDIR /app`**  Writes to the config: *"Start the user in this directory."*
* **`USER 1001`**  Writes to the config: *"Switch to user ID 1001 before running anything."*

**Result:** These add 0 bytes to the image size. They just edit a small JSON file (the Config) that accompanies the layers.

**Summary**:  

| Dockerfile Instruction | Type | Effect on Image | Where it lives |
| --- | --- | --- | --- |
| `RUN pip install numpy` | **Builder** | Adds 50MB | In a **Layer** (tar.gz) |
| `EXPOSE 8080` | **Declarative** | Adds 0 bytes | In the **Manifest/Config** (JSON) |
| `COPY source/ .` | **Builder** | Adds 2MB | In a **Layer** (tar.gz) |
| `ENTRYPOINT ["/bin/app"]` | **Declarative** | Adds 0 bytes | In the **Manifest/Config** (JSON) |

So, when you write a Dockerfile, you are simultaneously scripting the **construction** of the filesystem (Layers) and the **configuration** of the runtime environment (Manifest).

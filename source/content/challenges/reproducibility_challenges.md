{% if build == "slides" %}
# Transparency & Reproducibility
{% else %}
## Ensuring Reproducible and Transparent Research
{% endif %}

{% if slide %}
**Scientific integrity requires reproducible computational work**

**Why reproducibility matters:**
- Validates scientific claims
- Enables building on previous work
- Facilitates collaboration and review
- Increases research impact
{% endif %}

{% if page %}
Computational reproducibility is the ability to obtain consistent results using the same data and code. It is fundamental to scientific integrity. However, achieving reproducibility in computational research presents substantial challenges.

Studies have shown that many published computational results cannot be reproduced, even when researchers attempt to reproduce their own work from months or years earlier. This reproducibility crisis undermines the scientific process and wastes resources.

Reproducibility serves multiple purposes:

- **Validation**: Others can verify computational results
- **Extension**: Future work can build on verified methods
- **Transparency**: Reviewers and readers can understand exactly what was done
- **Error detection**: Reproducibility attempts may reveal bugs or errors
- **Collaboration**: Team members can work with consistent workflows

The challenge is that achieving reproducibility requires intentional effort throughout a project.
{% endif %}

{% if build == "slides" %}
---
{% else %}
### Creating Reproducible Workflows
{% endif %}

:::{admonition} Reproducibility vs. Replicability
:class: margin
**Reproducibility**: Same results with same data/code  
**Replicability**: Consistent findings with new data/independent study
:::

:::{admonition} Reproducibility vs. Replicability
:class: margin
**Reproducibility**: Same results with same data/code  
**Replicability**: Consistent findings with new data/independent study
:::

{% if slide %}
**Many factors affect whether work can be reproduced**
**Best practices require effort:**
- Automated pipelines instead of manual steps
- Explicit parameter documentation
- Version control for all code and scripts
- Clear documentation of the complete workflow
{% endif %}

{% if page %}
Reproducible workflows don't happen by accident. They require conscious design choices and documentation practices.

### Documentation Requirements

Reproducing computational work requires knowing:

- **Exact steps performed**: What commands were run, in what sequence
- **Parameters and settings**: All configuration choices that affect results
- **Input data specifications**: What data was used, including versions and preprocessing
- **Decision points**: How ambiguous situations or edge cases were handled

Incomplete documentation makes reproduction difficult or impossible. The challenge is that documenting everything feels like overhead during active research, but becomes critical when attempting to reproduce work later.

### Workflow Design Decisions

The structure of computational workflows affects reproducibility:

- **Manual steps**: Interactive data exploration and ad-hoc analysis are difficult to reproduce exactly. What seemed obvious at the time may not be obvious later.
- **Implicit dependencies**: If scripts rely on specific file locations, environment variables, or system state, these dependencies may not be apparent to someone attempting reproduction.
- **Non-deterministic elements**: Some algorithms involve randomness. Without setting random seeds, results will vary between runs.

Reproducible workflows favor automation, explicit configuration, and deterministic execution where possible. This requires upfront investment in infrastructure and discipline.
{% endif %}

{% if build == "slides" %}
---
{% else %}
### Environment Consistency
{% endif %}

{% if slide %}
**Software and hardware environments critically affect results**

:::{admonition} "It Works on My Machine"
:class: warning
Environment inconsistencies are a primary cause of reproducibility failures
:::
{% endif %}

{% if page %}
Computational results depend not just on code and data, but on the complete software and hardware environment in which computation runs.

### Software Environment Challenges

Software environments are complex ecosystems with many components:

**Version dependencies**: Scientific software typically depends on libraries (NumPy, SciPy, TensorFlow, etc.), which themselves depend on other libraries. Each component has multiple versions, and behavior can change between versions. A calculation that works with library version 1.2 might produce different results (or fail entirely) with version 1.3.

**Operating system differences**: System libraries, file handling, and process management differ between operating systems. Code developed on Linux may behave differently on macOS or Windows.

**Compiler effects**: For compiled languages or libraries with compiled components, different compilers or optimization levels can produce subtly different numerical results due to instruction ordering or precision handling.

The challenge is that tracking and reproducing the complete software environment is not straightforward. Simply knowing "I used Python" is insufficient; you need specific versions of Python, all installed packages, and potentially system libraries.

### Hardware Variability

Even with identical code and software, hardware differences can affect results:

**Floating-point arithmetic**: Different CPU architectures may handle floating-point operations slightly differently, particularly for edge cases. Accumulating small differences across billions of operations can lead to noticeable divergence.

**Parallel execution**: The order in which parallel operations complete may vary between runs or systems, leading to non-deterministic results if operations aren't carefully ordered.

**GPU computing**: Different GPU models or drivers may produce subtly different results, particularly in reduced-precision operations.

Perfect bit-for-bit reproducibility across all hardware is often not achievable. The goal becomes ensuring scientifically meaningful reproducibility: results that match within acceptable tolerances.
{% endif %}

{% if build == "slides" %}
---
{% else %}
### Data Transparency and Availability
{% endif %}

{% if slide %}
**Results depend on data—but sharing is complex**
**Mitigation strategies:**

✓ Share subsets or synthetic data  
✓ Document data characteristics  
✓ Provide preprocessing code  
✓ Describe model training data properties

{% endif %}

{% if page %}
Reproducibility requires access to the data used in computation. However, data sharing presents its own challenges.

### Data Sharing Barriers

Several factors limit data availability:

**Size constraints**: Large datasets (hundreds of gigabytes or terabytes) are difficult to share. Storage and bandwidth costs make wholesale data sharing impractical in many cases.

**Privacy and sensitivity**: Research involving human subjects, proprietary information, or sensitive data cannot be freely shared due to ethical or legal constraints.

**Intellectual property**: Data may represent significant investment and competitive advantage, limiting sharing incentives.

**Data rights**: Researchers may not have permission to share data obtained from other sources.

### Preprocessing and Provenance

Even when raw data is available, reproducibility requires documenting all preprocessing and transformation steps. Data cleaning, normalization, feature extraction, and filtering all affect results. If these steps aren't documented or provided in executable form, reproducing results becomes difficult.

### Pre-trained Models

Machine learning introduces additional complexity. Pre-trained models represent the compressed knowledge from training data, but the training data itself may not be available. This creates challenges:

- **Black-box uncertainty**: Understanding what the model learned and its limitations requires knowing about training data
- **Bias propagation**: Biases in training data affect model behavior, but aren't visible without access to that data
- **Domain applicability**: Knowing whether a pre-trained model applies to a new domain requires understanding the training data distribution

Transparency in data (or at minimum, comprehensive documentation of data characteristics, sources, and preprocessing) is essential for meaningful reproducibility.
{% endif %}

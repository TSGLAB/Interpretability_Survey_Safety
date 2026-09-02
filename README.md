# Interpretability for AI Safety Survey: Interactive Notebooks

## Overview

These notebooks provide hands-on implementations of key  interpretability techniques. Each notebook is self-contained with explanations, code, and exercises — designed to build intuition for how these methods work and when to apply them.

The notebooks progress from foundational concepts to safety-relevant applications.

*Recommended order:** Notebooks are numbered intentionally. Within each section, start with `01_` and progress sequentially.

**Dependencies:**
- `01_core_hypotheses/` → Foundation for everything else. Start here.
- `02_feature_extraction/` → Requires understanding of superposition (01_02)
- `03_circuits/` → Builds on feature extraction concepts
- `04_intermediate_computation/` → Largely independent, can be done in parallel
- `05_representation_analysis/` → Requires circuits and intermediate computation
- `06_safety_applications/` → Capstone; assumes familiarity with prior sections



[![Python 3.11+](https://img.shields.io/badge/python-3.11+-blue.svg)](https://www.python.org/downloads/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Interactive Python notebooks for understanding AI interpretability concepts, focusing on mechanistic interpretability (MI) for AI safety. Companion materials for **"The State of Interpretability for AI Safety: Survey of Foundations, Methods, and Research Directions"**.

---

## 📁 Repository Structure

```
notebooks/
├── 01_core_hypotheses/
│   ├── 01_linear_representation_hypothesis.ipynb
│   ├── 02_superposition_hypothesis.ipynb
│   └── 03_privileged_access_hypothesis.ipynb
│
├── 02_feature_extraction/
│   ├── 01_sparse_autoencoders_basics.ipynb
│   ├── 02_transcoders.ipynb
│   └── 03_crosscoders.ipynb
│
├── 03_circuits/
│   ├── 01_circuit_discovery.ipynb
│   └── 02_causal_verification.ipynb
│
├── 04_intermediate_computation/
│   ├── 01_logit_lens.ipynb
│   ├── 02_tuned_lens.ipynb
│   ├── 03_jacobian_lens.ipynb
│   ├── 04_patchscopes.ipynb
│   ├── 05_probing_classifiers.ipynb
│   ├── 06_activation_oracles.ipynb
│   └── 07_natural_language_autoencoders.ipynb
│
├── 05_representation_analysis/
│   ├── 01_model_diffing.ipynb
│   ├── 02_knowledge_localization.ipynb
│   └── 03_representation_engineering.ipynb
│
└── 06_safety_applications/
    ├── 01_concept_erasure.ipynb
    └── 02_steering_vectors.ipynb
```

---

## 🛠️ Environment Setup

```bash
# Create and activate conda environment
conda create -n misurvey python=3.11 -y
conda activate misurvey

# Install dependencies
pip install -r ./requirements.txt
```

---

## 📖 Notebook Descriptions

### Core Hypotheses (`01_core_hypotheses/`)

| Notebook | Description |
|----------|-------------|
| **01_linear_representation_hypothesis** | Concepts as linear directions in activation space. Visualization and probing experiments. |
| **02_superposition_hypothesis** | How networks represent more features than neurons. Toy models and geometry. |
| **03_privileged_access_hypothesis** | Privileged bases and when neurons align with interpretable features. |
| **04_universality_platonic_representation** | Universal representations across models and the Platonic representation hypothesis. |

### Feature Extraction (`02_feature_extraction/`)

| Notebook | Description |
|----------|-------------|
| **01_sparse_autoencoders_basics** | Build and train SAEs from scratch. Core principles of sparse feature extraction. |
| **02_transcoders** | Bridging nonlinear MLP layers. Learn MLP input→output mappings in feature space. |
| **03_crosscoders** | Cross-layer feature analysis. Track features across multiple layers. |

### Circuits (`03_circuits/`)

| Notebook | Description |
|----------|-------------|
| **01_circuit_discovery** | Activation patching, path patching, and automatic circuit discovery methods. |
| **02_causal_verification** | Causal scrubbing and intervention techniques to verify circuit hypotheses. |

### Intermediate Computation (`04_intermediate_computation/`)

| Notebook | Description |
|----------|-------------|
| **01_logit_lens** | Project intermediate representations to vocabulary space. |
| **02_tuned_lens** | Learned per-layer transforms for better intermediate decoding. |
| **03_jacobian_lens** | The Jacobian lens — measures the model's average Jacobian to read verbalizable representations from intermediate layers. Follows the official walkthrough; includes fitting and R-lens. |
| **04_patchscopes** | Use the LM itself to explain its intermediate representations. |
| **05_probing_classifiers** | Linear probes, control tasks, and causal limitations of probing. |
| **06_activation_oracles** | Training LLMs to explain their own activations (LatentQA). |
| **07_natural_language_autoencoders** | Read an activation as free-form English via a released NLA (verbalizer + reconstructor). Follows the official repo — inference over an SGLang server, with reconstruction/FVE scoring. |

### Representation Analysis (`05_representation_analysis/`)

| Notebook | Description |
|----------|-------------|
| **01_model_diffing** | Compare representations across model versions and architectures. |
| **02_knowledge_localization** | Where is factual knowledge stored? Causal tracing and ROME. |
| **03_representation_engineering** | Steering vectors and activation manipulation for behavior control. |

### Safety Applications (`06_safety_applications/`)

| Notebook | Description |
|----------|-------------|
| **01_concept_erasure** | Remove specific concepts/capabilities from models (LEACE, PISCES). |
| **02_steering_vectors** | Practical behavioral control through activation interventions. |

---

## 🚀 Getting Started

```bash
# Clone and setup
Download this folder
cd Interpretability_Survey_Safety
pip install -r requirements.txt
```

### Requirements

```
torch>=2.0.0
transformers>=4.35.0
numpy>=1.24.0
matplotlib>=3.7.0
einops>=0.7.0
transformer-lens>=1.0.0
```

---

##  Related Resources

- [TransformerLens](https://github.com/neelnanda-io/TransformerLens)
- [SAELens](https://github.com/jbloomAus/SAELens)
- [transformer-circuits.pub](https://transformer-circuits.pub)

---


## 📜 License

MIT License - see [LICENSE](LICENSE) for details.

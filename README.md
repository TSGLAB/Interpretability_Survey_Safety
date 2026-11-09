# Interpretability for AI Safety Survey: Interactive Notebooks

[![Python 3.11+](https://img.shields.io/badge/python-3.11+-blue.svg)](https://www.python.org/downloads/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Companion notebooks for **"Understanding AI from the Inside: The State of Mechanistic Interpretability for AI Safety"**, focusing on mechanistic interpretability (MI) for AI safety.

[Paper (arXiv:2611.08438)](https://arxiv.org/abs/2611.08438) · [Project page](https://tsglab.github.io/mechinterp-safety/)

## Overview

These notebooks provide hands-on implementations of key interpretability techniques. Each notebook is self-contained with explanations, code, and exercises — designed to build intuition for how these methods work and when to apply them.

The notebooks progress from foundational concepts to safety-relevant applications.

**Recommended order:** Notebooks are numbered intentionally. Within each section, start with `01_` and progress sequentially.

**Dependencies:**
- `01_core_hypotheses/` → Foundation for everything else. Start here.
- `02_feature_extraction/` → Requires understanding of superposition (01_02)
- `03_circuits/` → Builds on feature extraction concepts
- `04_intermediate_computation/` → Largely independent, can be done in parallel
- `05_representation_analysis/` → Requires circuits and intermediate computation
- `06_safety_applications/` → Capstone; assumes familiarity with prior sections

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
│   └── 01_circuit_discovery.ipynb
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

## 🛠️ Setup

```bash
git clone https://github.com/fbarez/Interpretability_Survey_Safety.git
cd Interpretability_Survey_Safety

conda create -n misurvey python=3.11 -y
conda activate misurvey
pip install -r requirements.txt

jupyter notebook notebooks/
```

See [`requirements.txt`](requirements.txt) for the full dependency list.

### Running on Google Colab

Most notebooks run on a free Colab runtime (CPU or T4 GPU) via the "Open in Colab" links on the
[project page](https://tsglab.github.io/mechinterp-safety/notebooks/), which also lists each notebook's hardware needs.
The exceptions:

| Notebook | Needs |
|----------|-------|
| `01_core_hypotheses/03_privileged_access_hypothesis` | ~32 GB GPU (A100); gated `meta-llama/Llama-3.1-8B`. Clones this repo automatically for its `model/` and `demo_data/` folders. |
| `04_intermediate_computation/07_natural_language_autoencoders` | ~40 GB GPU plus a separately launched SGLang server; not runnable on free Colab. |
| `05_representation_analysis/01_model_diffing` | Gated `google/gemma-2-2b` / `gemma-2-2b-it`. |
| `05_representation_analysis/03_representation_engineering` | Part 2: ~26 GB GPU (A100); gated `meta-llama/Llama-2-13b-chat-hf`. Part 1 runs on CPU. |

For gated models, accept the licence on the model's Hugging Face page, then add your token as `HF_TOKEN` in Colab's
🔑 Secrets panel (or run `huggingface-cli login` locally). The notebooks pick it up automatically.

---

## 📖 Notebook Descriptions

### Core Hypotheses (`01_core_hypotheses/`)

| Notebook | Description |
|----------|-------------|
| **01_linear_representation_hypothesis** | Concepts as linear directions in activation space. Visualization and probing experiments. |
| **02_superposition_hypothesis** | How networks represent more features than neurons. Toy models and geometry. |
| **03_privileged_access_hypothesis** | Can a model explain its own internals better than other models can? Compares self- vs. external explainers on residual-stream and SAE feature descriptions. |

### Feature Extraction (`02_feature_extraction/`)

| Notebook | Description |
|----------|-------------|
| **01_sparse_autoencoders_basics** | Implement five SAE variants (ReLU, Gated, JumpReLU, Top-K, Batch Top-K) and compare them on synthetic data with known ground-truth features. |
| **02_transcoders** | Bridging nonlinear MLP layers. Train a transcoder and a cross-layer transcoder on toy MLPs with known structure. |
| **03_crosscoders** | Cross-layer feature analysis. Use per-layer decoder norms to separate persistent from layer-local features. |

### Circuits (`03_circuits/`)

| Notebook | Description |
|----------|-------------|
| **01_circuit_discovery** | Activation patching, path patching, and automatic circuit discovery methods. |

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
| **01_concept_erasure** | Remove a concept from GPT-2's activations with a LEACE-style projection; a lightweight baseline for the PISCES pipeline. |
| **02_steering_vectors** | Practical behavioral control through activation interventions. |

---

## 🔗 Related Resources

- [TransformerLens](https://github.com/neelnanda-io/TransformerLens)
- [SAELens](https://github.com/jbloomAus/SAELens)
- [transformer-circuits.pub](https://transformer-circuits.pub)

---

## 📝 Citation

If you use these notebooks, please cite the survey:

```bibtex
@misc{barez2026understandingaiinsidestate,
      title={Understanding AI from the Inside: The State of Mechanistic Interpretability for AI Safety}, 
      author={Fazl Barez and Tung-Yu Wu and Hunar Batra and Gabriele Dominici and Florent Draye and Yanai Elazar and Damiano Fornasiere and Antía García and Abir Harrasse and Riley Harris and Sara Hooker and Michael Lan and Belinda Z. Li and Aaron Maiwald and Narmeen Fatimah Oozeer and Naomi Saphra and Or David Shafran and Adi Simhi and Robert Trager and Shriyash Kaustubh Upadhyay and Ziyu Yao and Yu Zhao and Shay B. Cohen and Mor Geva and Yoshua Bengio and Stella Biderman and Hassan Sajjad},
      year={2026},
      eprint={2611.08438},
      archivePrefix={arXiv},
      primaryClass={cs.CL},
      url={https://arxiv.org/abs/2611.08438}, 
}
```

---

## 📜 License

MIT License.

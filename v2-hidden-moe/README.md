# Hidden Mixture-of-Experts: Emergent Bipolar Routing in Dense Transformers

**DOI**: [10.5281/zenodo.17381003](https://doi.org/10.5281/zenodo.17381003)
**Date**: October 18, 2025  
**Author**: Seungho Choi  
**Extends**: [v1.0: Geometric Interpretability](https://doi.org/10.5281/zenodo.17355345)

---

## 🎯 TL;DR

We discover that standard transformer models (Llama-2, Mistral, Qwen-2.5) **already implement mixture-of-experts-style routing**—without any explicit MoE architecture. Tasks organize into completely separate neural circuits (0% overlap), achieving extreme sparsity (2 neurons suffice for 97.7% accuracy) and enabling 72% computational reduction.

---

## 📄 Paper

- **PDF**: [`paper.pdf`](./paper.pdf)
- **LaTeX**: [`paper.tex`](./paper.tex)
- **Figures**: [`figures/`](./figures/)

---

## 🔬 Key Findings

### 1. Perfect Spatial Separation (0% Overlap)
```
Llama-2-7B:    Certainty ∩ Sentiment = ∅
Mistral-7B:    Certainty ∩ Sentiment = ∅
Qwen-2.5-7B:   Certainty ∩ Sentiment = ∅
```

Tasks occupy completely disjoint neural circuits across all three models.

### 2. Extreme Neural Sufficiency

| Neurons | Accuracy | % of Model |
|---------|----------|------------|
| 1       | 97.6%    | 0.00076%   |
| **2**   | **97.7%**| **0.0015%**|
| 5       | 97.7%    | 0.0038%    |
| 10      | 97.8%    | 0.0076%    |

Just **2 neurons** (Layer 9, positions 3842 & 3944) achieve near-perfect binary classification.

### 3. Task-Specific Specialization

Cross-task performance matrix:

|          | Certainty Task | Sentiment Task |
|----------|----------------|----------------|
| **Certainty Neurons** | 86.3% ✅ | 51.3% ❌ |
| **Sentiment Neurons** | 45.4% ❌ | 74.8% ✅ |

Diagonal dominance = strong specialization (1.6-1.8× ratios).

### 4. Early Exit Potential

**Mistral-7B Certainty Task**:
- Layers 0-8 (28% compute): **96.7%** accuracy
- Layers 0-31 (100% compute): **96.7%** accuracy
- **Result**: 0% degradation, **72% compute reduction**

---

## 🎨 Visualizations

### Multi-Model Comparison

![Multi-Model](./figures/multi_model_comparison.png)

*Universal structure across Llama, Mistral, Qwen*

### Complete Circuit Dashboard

![Dashboard](./figures/complete_circuit_dashboard.png)

*Mistral-7B detailed analysis*

### Layer Architecture

![Architecture](./figures/circuit_layer_architecture.png)

*Spatial separation: parallel pathways with zero connections*

---

## 🧩 Relation to v1.0

### Evolution of Ideas

| Aspect | v1.0 (Bipolar Detection) | v2.0 (Hidden MoE) |
|--------|---------------------------|-------------------|
| **Discovery** | Bipolar activation patterns | Universal circuit organization |
| **Scope** | Single model (Mistral) | Three models (Llama, Mistral, Qwen) |
| **Tasks** | Truth vs. Hallucination | Multi-task (Certainty + Sentiment) |
| **Focus** | Detection accuracy | Routing mechanisms |
| **Method** | Geometric boundaries | Circuit discovery |
| **Key Metric** | 100% detection accuracy | 0% overlap, 2-neuron sufficiency |

### Conceptual Bridge

v1.0 discovered that **bipolar encoding** enables perfect linear separation.

v2.0 reveals this is part of a larger phenomenon: **tasks self-organize into disjoint circuits** with MoE-like routing properties.

---

## 📖 Citation
```bibtex
@article{choi2025hiddenmoe,
  title={Hidden Mixture-of-Experts: Emergent Bipolar Routing in Dense Transformers},
  author={Choi, Seungho},
  year={2025},
  month={October},
  publisher={Zenodo},
  doi={10.5281/zenodo.17381003},
  note={Extends: \url{https://doi.org/10.5281/zenodo.17355345}}
}
```

---

## 📧 Contact

**Seungho Choi**  
Independent Researcher  
Email: madst0614@gmail.com

Feedback, questions, and collaboration inquiries welcome!

---

## 📄 License

- **Paper**: CC BY 4.0
- **Code**: MIT
- **Figures**: CC BY 4.0
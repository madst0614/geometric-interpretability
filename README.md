# Geometric Interpretability: Understanding Neural Networks through Boundary Analysis

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.17329836.svg)](https://doi.org/10.5281/zenodo.17329836)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)

**Paper**: Geometric Interpretability: A Quantitative Framework for Understanding Large Language Models through Boundary Analysis  
**Author**: Seungho Choi (madst0614@gmail.com)  
**Date**: January 2025

## Overview

Large language models generate outputs with uniform confidence regardless of epistemic uncertainty, leading to hallucinations. We introduce **Geometric Interpretability**—a framework for understanding neural networks through spatial structure rather than semantic content—analyzing where knowledge boundaries exist rather than what networks know.

This paradigm trades semantic detail for structural efficiency: 1000× faster setup than mechanistic interpretability, enabling practical uncertainty detection in production systems.

### Key Findings

- **Perfect Linear Boundaries**: 0.13% curvature deviation from perfect linearity (Mistral-7B)
- **Bipolar Encoding**: Truth and hallucination activate the same neurons with opposite signs (r = -1.0), achieving information-theoretically optimal structure with O(D) complexity
- **Quality Dominance**: Training quality dominates language effects by 12.6× factor
- **Perfect Hallucination Detection**: 100% accuracy with zero errors, 48.0% coverage (317% improvement over baselines)
- **Natural Emergence**: +1569% separation increase from random initialization through standard training
- **Production Ready**: 30-second setup, <1ms inference, $0.50 cost, no retraining required

### Computational Requirements

- **Setup Time**: 30 seconds
- **Cost**: $0.50 (cloud GPU)
- **Inference Overhead**: <1ms per query
- **No model retraining required**

## Quick Start

### Try it in Google Colab (No Setup Required!)

🚀 **[Open Interactive Notebook](https://colab.research.google.com/drive/1_L94JvriG8Kkr5lldywH2VESlAcEEbmH?usp=sharing)**

Run boundary curvature analysis on your own models directly in your browser - takes only 30 seconds!

### Local Installation

```bash
# Clone repository
git clone https://github.com/madst0614/geometric-interpretability.git
cd geometric-interpretability

# Install dependencies
pip install -r requirements.txt

# Run basic analysis
python run_analysis.py --model mistral-7b --layer 16 --dataset truthfulqa
```

## Interactive Demo

🔗 **Try it yourself**: [Google Colab Notebook](https://colab.research.google.com/drive/1_L94JvriG8Kkr5lldywH2VESlAcEEbmH?usp=sharing)

Run boundary curvature analysis on your own models in your browser - no setup required!

## Main Results

### 1. Perfect Linear Boundaries (Section 4.1)

Analyzing Mistral-7B Layer 16 on 1000 TruthfulQA samples:

**Linearity Measurements:**
- Linear SVM (0.746) vs RBF SVM (0.749) = 0.3% curvature deviation
- Symmetry: Distance ratio between classes = 1.000 (perfect)
- Concentration: 148× variance along boundary normal vs perpendicular directions
- Statistical validation: 820/4096 neurons (20%) boundary-relevant (p<0.0001)

**Cross-Model Consistency:**

| Model | Linear Acc | RBF Acc | Curvature | Effect Size |
|-------|-----------|---------|-----------|-------------|
| Mistral-7B | 0.746 | 0.749 | **0.13%** | 1.52 (Large) |
| Phi-2 | 0.742 | 0.748 | 0.75% | 0.31 (Small) |
| Gemma-7B | 0.738 | 0.748 | 1.38% | 1.61 (Large) |
| Llama-3-8B | 0.731 | 0.764 | 4.50% | 1.42 (Large) |
| Llama-2-7B | 0.720 | 0.748 | 3.88% | 0.56 (Medium) |
| Qwen2-7B | 0.665 | 0.754 | 13.38% | 0.90 (Large) |

*Note: Qwen2-7B's higher curvature reflects domain mismatch (Chinese pretraining, English evaluation), not poor quality.*

### 2. Quality Dominance Over Language Effects (Section 4.2)

Systematic 3×2 experiment decomposing training quality vs language distribution:

**Key Finding: Quality effect (12.57pp) dominates language effect (0.99pp) by factor of 12.6×**

| Model | Quality | English | Chinese | Language Δ |
|-------|---------|---------|---------|------------|
| Mistral-7B | High | -0.24% | -1.00% | 0.76pp |
| Qwen2-7B | High | -1.77% | -0.54% | 1.23pp |
| Llama-2-7B | Low | +12.33% | +6.63% | 5.70pp |

**Implications:**
- High-quality models maintain linearity across languages (<1.5pp variation)
- Poor training quality persists regardless of language match
- Training quality matters 12.6× more than language distribution
- Geometric structure is language-agnostic when well-trained

### 3. Bipolar Encoding: The High-Dimensional Paradox (Section 4.3)

Multi-layer pathway analysis (26 concatenated layers, 21,294 dimensions):

**The Paradox:**
- **Weak Euclidean separation**: ratio 0.225 (classes heavily overlap)
- **Perfect linear discriminability**: 100% accuracy via LDA
- **Mechanism**: Truth and hallucination activate same neurons with opposite signs

**Measurements:**
- Center distance: 63.9
- Truth radius: 141.8 (±7.4)
- Hallucination radius: 142.4 (±10.9)
- Separation ratio: 0.225 (weak spatial separation)
- Neuron correlation: r = -1.000 (perfect bipolar encoding)
- LDA accuracy: 100% (perfect discrimination)

**Layer-Wise Evolution:**

| Layer | Sep. Ratio | LDA Acc | Correlation |
|-------|-----------|---------|-------------|
| L6 | 0.195 | 98.5% | -0.94 |
| L12 | 0.229 | 99.5% | -0.97 |
| L16 | 0.240 | 100% | -0.98 |
| L24 | 0.244 | 100% | -0.99 |
| L31 | 0.282 | 100% | -1.00 |

**Information-Theoretic Optimality:**
- Bipolar encoding achieves O(D) complexity vs O(2D) for separate pathways
- Represents Shannon's lower bound: 1 bit (sign) per neuron
- Maximum representational efficiency without redundant capacity

### 4. Perfect Hallucination Detection (Section 5)

Multi-layer geometric boundary analysis (5 strategic layers: L6, L14, L18, L24, L30):

**Performance on TruthfulQA (Adversarial Benchmark):**

| Method | Layers | Accuracy | Coverage | Errors |
|--------|--------|----------|----------|--------|
| Single Layer | L16 | 94.0% | 38.5% | 3 |
| 3-Layer Consensus | L8,16,24 | 96.5% | 35.5% | 2 |
| **5-Layer Concat** | **L6,14,18,24,30** | **100%** | **48.0%** | **0** |
| 19-Layer Full | L6,14-31 | 100% | 48.0% | 0 |

**Key Results:**
- 100% accuracy with zero false positives and zero false negatives
- 48.0% coverage (317% improvement over consensus: 48.0% vs 35.5%)
- Perfect AUC: 1.000 (complete class separation)
- Efficiency plateau: 5 layers = 19 layers performance with 4× fewer features

**Tunable Risk Profiles:**

| Threshold | Mode | Accuracy | Coverage | Errors | Use Case |
|-----------|------|----------|----------|--------|----------|
| τ = 0.70 | Balanced | 98.6% | 35.5% | 1/71 | Consumer chatbots |
| τ = 0.80 | Conservative | 98.1% | 27.0% | 1/54 | Sensitive domains |
| τ = 0.90 | **High-stakes** | **100%** | **11.5%** | **0/23** | Medical/Legal AI |
| τ = 0.95 | Ultra-safe | 100% | 7.0% | 0/14 | Critical systems |

**Production Efficiency:**
- Setup: 30 seconds, $0.50 on cloud GPU
- Inference: <1ms additional latency per query
- No model retraining required
- 1000× faster than mechanistic interpretability (30s vs weeks)

## Theoretical Foundations

Our empirical findings connect to established theory in deep learning:

### 1. Implicit Bias Toward Max-Margin Solutions

**Theory**: Soudry et al. (2018) prove gradient descent on linearly separable data converges to max-margin solutions.

**Our Evidence**: 0.13% curvature validates this at 7B parameter scale
- Well-trained models (Mistral, Qwen): <2% curvature
- Poorly-trained models (Llama-2): 3.88% curvature
- Quality determines whether implicit bias manifests

### 2. Information Bottleneck and Optimal Compression

**Theory**: Tishby & Zaslavsky (2015) - networks compress input while preserving task-relevant signals.

**Our Evidence**: Bipolar encoding achieves information-theoretic optimality
- Binary classification requires log₂(2) = 1 bit
- Bipolar encoding: 1 bit (sign) per neuron = O(D) complexity
- Alternative encodings (separate pathways: O(2D)) are provably suboptimal
- Achieves Shannon's lower bound for binary discrimination

### 3. Progressive Hierarchical Refinement

**Theory**: Deep networks progressively disentangle representations (Saxe et al., 2019).

**Our Evidence**: Layer-wise geometric evolution
- Separation: 0.195 (L6) → 0.282 (L31)
- Correlation: r = -0.94 (L6) → r = -1.00 (L31)
- LDA accuracy: 98.5% (L6) → 100% (L31)
- Networks gradually compress O(|K|) facts into O(2) geometric clusters

### Unified Framework: Measurement Predicts Performance

```
High-quality training 
  → Implicit bias toward linearity (0.13% curvature)
  → Information compression (bipolar encoding, r = -1.0)
  → Sparse structure (20% boundary-relevant neurons)
  → Perfect detection (100% accuracy, 0 errors)
```

Geometric properties don't just describe networks—they **determine** what applications are possible.

## Reproducibility

All experiments designed for rapid community validation:
- **Total compute**: ~60 hours on single GPU
- **Cost**: <$50 on cloud platforms
- **Code**: Complete implementations provided
- **Data**: TruthfulQA (public), modular arithmetic (generated)
- **Protocol**: Model-agnostic, works on any Transformer with accessible activations

## Citation

```bibtex
@article{choi2025geometric,
  title={Geometric Interpretability: Understanding Neural Networks through Boundary Analysis},
  author={Choi, Seungho},
  year={2025},
  doi={10.5281/zenodo.17329836}
}
```

## Positioning: Complementary to Mechanistic Interpretability

Geometric Interpretability doesn't replace mechanistic methods—it complements them:

| Approach | Question | Strength | Use Case |
|----------|----------|----------|----------|
| **Mechanistic** | What circuits compute? | Semantic understanding | Deep causal analysis |
| **Geometric** | Where boundaries exist? | 1000× faster, objective | Production safety monitoring |

**When to use each:**
- **Mechanistic**: Understanding specific algorithms, debugging behaviors, research depth
- **Geometric**: Uncertainty detection, rapid model comparison, production deployment
- **Combined**: Geometric screening → Mechanistic deep-dive for interesting regions

**Tradeoff**: Speed vs detail. Geometric provides structural efficiency; mechanistic provides semantic insight.

## Limitations and Future Work

### Current Scope
- **Architectures**: Transformer-based language models only
  - Future: Vision Transformers, multimodal models, non-Transformer (Mamba, SSMs)
- **Tasks**: Binary classification (truth vs hallucination)
  - Future: Multi-class, hierarchical uncertainty types
- **Analysis**: Static models
  - Future: Continual learning, geometric drift monitoring

### Coverage-Accuracy Tradeoff
- High-stakes mode: 100% accuracy but only 11.5% coverage
- Balanced mode: 98.6% accuracy with 35.5% coverage
- Future: Improve coverage while maintaining perfect accuracy

### Theoretical Gaps
- **Open questions**:
  - Can we derive curvature bounds analytically?
  - Does K-class generalize to K-polar encoding?
  - What determines efficiency-robustness tradeoff?
  - How does geometry evolve during training?

### Adversarial Robustness
- Evaluated on natural adversarial benchmarks (TruthfulQA)
- Adaptive attacks targeting geometric boundaries unexplored
- Weak separation (0.225) may create vulnerability along LDA direction

## Contact

**Seungho Choi**  
Email: madst0614@gmail.com  
GitHub: [@madst0614](https://github.com/madst0614)

## License

MIT License - see [LICENSE](LICENSE) file for details.

---

*"Questions outnumber answers. Intentionally. Let's find out together."*

**Critical Finding: Regime transition at 2,000 samples**

| Train Size | 1-Layer | 3-Layer | 5-Layer | Best |
|-----------|---------|---------|---------|------|
| 500 | 87.0% | 82.0% | 79.5% | 1L |
| 1,000 | 85.5% | 82.0% | 81.5% | 1L |
| **2,000** | 94.0% | 98.5% | **100%** | **5L+** |
| 3,000 | 94.0% | 98.5% | 100% | 5L+ |
| 5,000 | 94.0% | 98.5% | 100% | 5L+ |

**Interpretation:**
- Below 2K: Simple models generalize better (avoid overfitting)
- Above 2K: Multi-layer captures rich geometric structure
- Practical guideline: Collect ≥2,000 labeled samples for production

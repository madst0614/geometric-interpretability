# Geometric Interpretability: Understanding Neural Networks through Boundary Analysis

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.17329836.svg)](https://doi.org/10.5281/zenodo.17329836)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)

**Paper**: Geometric Interpretability: Understanding Neural Networks through Boundary Analysis  
**Author**: Seungho Choi (madst0614@gmail.com)  
**Date**: January 2025

## Overview

Large language models generate outputs with uniform confidence regardless of epistemic uncertainty, leading to hallucinations. We introduce **Geometric Interpretability**—a framework for understanding neural networks through spatial structure rather than semantic content—and propose **Geometric Boundary Analysis (GBA)** for detecting knowledge boundaries in activation space.

### Key Findings

- **Perfect Linear Boundaries**: 0.3% curvature deviation from perfect linearity, 1.000 symmetry ratio, 148× information concentration in a single dimension
- **Separation Dominance**: Class separation correlates more strongly with generalization (r=0.910, p<0.0001) than boundary sharpness (r=-0.651) during grokking
- **Practical Epistemic Routing**: 96.5% hallucination detection with multi-layer consensus, 98.6% accuracy in balanced mode (35.5% coverage), 100% accuracy in high-stakes mode (11.5% coverage) with zero false positives
- **Natural Emergence**: Training creates +1569% separation increase from random initialization without specialized procedures

### Computational Requirements

- **Setup Time**: 30 seconds
- **Cost**: $0.50 (cloud GPU)
- **Inference Overhead**: <1ms per query
- **No model retraining required**

## Quick Start

```bash
# Clone repository
git clone https://github.com/madst0614/geometric-interpretability.git
cd geometric-interpretability

# Install dependencies
pip install -r requirements.txt

# Run basic analysis
python run_analysis.py --model mistral-7b --layer 16 --dataset truthfulqa
```

## Main Results

### 1. Perfect Linear Boundaries (Section 4.1)

Analyzing Mistral-7B Layer 16 on 1000 TruthfulQA samples:
- **Linearity**: Linear SVM (0.746) vs RBF SVM (0.749) = 0.3% difference only
- **Symmetry**: Distance to truth center = 0.34, distance to hallucination center = 0.34 (ratio: 1.000)
- **Concentration**: 148× variance along boundary normal vs perpendicular directions
- **Statistical validation**: 820/4096 neurons (20%) identified as boundary-relevant (p<0.0001)

### 2. Separation Dominance (Section 4.2)

Grokking experiment on modular arithmetic ((a+b) mod 97):
- During grokking (epoch 3000→3500): boundaries become **thicker** (+7.6%) while accuracy **improves** (+31.4%)
- Resolution: separation increases faster (+173%) than thickness
- **Correlation analysis**: Separation r=0.910 (p<0.0001) vs Sharpness r=-0.651 (p=0.0047)
- **Feature importance**: Separation +0.397 (dominant), Sharpness -0.058 (negligible)
- **Efficiency metric**: separation/thickness achieves r=0.965 correlation with accuracy

### 3. Distance-Based Epistemic Routing (Section 4.3)

Multi-layer consensus (Layers 8, 16, 24) on TruthfulQA:
- Single layer: 94.0% accuracy
- Multi-layer: 96.5% accuracy (+2.5% improvement)

**Threshold calibration** (tunable risk profiles):
- **Balanced mode** (τ=0.70): 98.6% accuracy, 35.5% coverage, 1/71 errors
- **Conservative mode** (τ=0.80): 98.1% accuracy, 27.0% coverage, 1/54 errors  
- **High-stakes mode** (τ=0.90): 100% accuracy, 11.5% coverage, 0/23 errors ⭐

**Causal validation**: Suppressing 820 boundary-relevant neurons → 91.71% NLL reduction (4.64→0.38)

### 4. Training Dynamics (Section 4.4)

Comparing random vs trained models (modular arithmetic):
- Random init: 0.499 accuracy, 0.335 separation
- Trained model: 0.906 accuracy, 5.585 separation (+1569%)
- Efficiency remains stable (-4.3%), suggesting proportional scaling

**Boundary maximization failure**: Explicit margin optimization produces 605× over-expansion, -8.0% accuracy drop—demonstrating natural training discovers better structure than direct geometric optimization.

## Repository Structure

```
geometric-interpretability/
├── data/                 # Datasets and processed activations
├── src/                  # Source code (analysis, experiments, utilities)
├── notebooks/            # Jupyter notebooks for visualization
├── results/              # Experimental outputs and figures
├── configs/              # Configuration files
└── paper.pdf            # Full paper
```

## Reproducibility

All experiments designed for rapid community validation:
- **Total compute**: ~60 hours on single GPU
- **Cost**: <$50 on cloud platforms
- **Code**: Complete implementations provided
- **Data**: TruthfulQA (public), modular arithmetic (generated)

## Citation

```bibtex
@article{choi2025geometric,
  title={Geometric Interpretability: Understanding Neural Networks through Boundary Analysis},
  author={Choi, Seungho},
  year={2025},
  doi={10.5281/zenodo.17329836}
}
```

## Positioning

Geometric Interpretability complements mechanistic interpretability:
- **Mechanistic**: "What does this circuit compute?" → Semantic understanding
- **Geometric**: "Where is this model uncertain?" → Structural safety
- **Tradeoff**: 1000× efficiency difference (weeks vs 30 seconds)

Use mechanistic methods for deep understanding; use geometric methods for rapid uncertainty detection in production.

## Contact

**Seungho Choi**  
Email: madst0614@gmail.com  
GitHub: [@madst0614](https://github.com/madst0614)

## License

MIT License - see [LICENSE](LICENSE) file for details.

---

*"Questions outnumber answers. Intentionally. Let's find out together."*
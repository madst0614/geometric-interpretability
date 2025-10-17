# Geometric Interpretability Research

A series of investigations into the internal organization of transformer language models, revealing hidden structure and emergent routing mechanisms.

---

## 📚 Papers

### 🆕 v2.0: Hidden Mixture-of-Experts (October 2025)

**Title**: Hidden Mixture-of-Experts: Emergent Bipolar Routing in Dense Transformers

**DOI**: [10.5281/zenodo.17381003](https://doi.org/10.5281/zenodo.17381003)

**Key Findings**:
- Perfect spatial separation (0% overlap) across Llama-2, Mistral, Qwen-2.5
- Task-specific circuits with 1.6-1.8× specialization ratios
- Just 2 neurons achieve 97.7% accuracy on binary classification
- 72% computational reduction via early-exit inference
- Universal MoE-like routing without explicit training

**Scope**: Multi-model, multi-task analysis demonstrating that standard transformers implicitly learn mixture-of-experts-style specialization

**Files**: [`v2-hidden-moe/`](./v2-hidden-moe/)

---

### v1.0: Geometric Interpretability (October 2025)

**Title**: Geometric Interpretability: A Quantitative Framework for Understanding Large Language Models through Boundary Analysis

**DOI**: [10.5281/zenodo.17355345](https://doi.org/10.5281/zenodo.17355345)

**Key Findings**:
- Discovery of bipolar activation patterns (r = -1.0)
- 100% hallucination detection accuracy
- Linear separability in high-dimensional space
- Geometric boundary analysis framework

**Scope**: Single-model analysis (Mistral-7B) focused on truth vs. hallucination detection

**Files**: [`v1-bipolar-detection/`](./v1-bipolar-detection/)

---

## 🔗 Research Evolution

This research represents a natural progression:
```
v1.0 (Foundation)
├─ Discovery: Bipolar neurons exist
├─ Task: Hallucination detection
├─ Model: Single (Mistral-7B)
└─ Method: Geometric boundary analysis

        ↓ Expansion

v2.0 (Generalization)
├─ Discovery: Hidden MoE structure (universal)
├─ Tasks: Multi-task analysis (certainty + sentiment)
├─ Models: Three architectures (Llama, Mistral, Qwen)
└─ Method: Circuit discovery + cross-task validation
```

The bipolar encoding mechanism identified in v1.0 proves to be a fundamental organizing principle underlying the hidden MoE structures revealed in v2.0.

---

## 📊 Visual Summary

### v2.0: Perfect Spatial Separation

![Multi-Model Comparison](./v2-hidden-moe/figures/multi_model_comparison.png)

*Zero neuron overlap across three independent model families*

### v2.0: Layer-by-Layer Architecture

![Circuit Architecture](./v2-hidden-moe/figures/circuit_layer_architecture.png)

*Parallel processing pathways with complete vertical separation*

---

## 📖 Citation

If you use this work, please cite the relevant version:

### v2.0 (Hidden MoE)
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

### v1.0 (Bipolar Detection)
```bibtex
@article{choi2025geometric,
  title={Geometric Interpretability: A Quantitative Framework for Understanding Large Language Models through Boundary Analysis},
  author={Choi, Seungho},
  year={2025},
  publisher={Zenodo},
  doi={10.5281/zenodo.17355345}
}
```

---

## 🤝 Contributing

This is independent research conducted in the open. Feedback, questions, and collaboration inquiries are welcome:

- **Email**: madst0614@gmail.com
- **Issues**: Use GitHub issues for technical questions
- **Discussions**: Use GitHub discussions for research ideas

---

## 📄 License

- **Papers**: Creative Commons Attribution 4.0 International (CC BY 4.0)
- **Code**: MIT License

---

## 🙏 Acknowledgments

Special thanks to the open-source community and the developers of:
- Hugging Face Transformers
- PyTorch
- The model organizations (Meta, Mistral AI, Alibaba)

---

**Author**: Seungho Choi (Independent Researcher)  
**Started**: 2025  
**Status**: Active research, papers under community review
# NumColor: Precise Numeric Color Control in Text-to-Image Generation

> **Accepted at ECCV 2026** 🎉

**[Muhammad Atif Butt](#)**, **[Diego Hernández](#)**, **[Alexandra Gomez-Villa](#)**, **[Kai Wang](#)**, **[Javier Vazquez-Corral](#)**, **[Joost van de Weijer](#)**

Computer Vision Center (CVC), Universitat Autònoma de Barcelona (UAB)

[![Paper](https://img.shields.io/badge/Paper-arXiv-b31b1b.svg)](https://arxiv.org/pdf/2603.13547)
[![Conference](https://img.shields.io/badge/ECCV-2026-blue.svg)](#)
[![Project Page](https://img.shields.io/badge/Project-Page-green.svg)](#)

---

## Overview

NumColor is a two-stage framework for **precise numerical color control** in text-to-image diffusion models. Given a natural language prompt containing hex color codes (e.g., `"a #FF5733 car next to a #2E86AB building"`), NumColor produces images whose object colors faithfully match the specified numeric values.

The framework introduces:

- **Color Token Aggregator (CTA):** A tokenizer-agnostic, learned module that detects and aggregates fragmented color tokens (hex codes / CSS-style color references) into coherent, injectable representations.
- **ColorBook:** A perceptually-structured color codebook trained on Lambertian-rendered data with calibrated D65 illumination, enabling precise mapping from numeric color specifications to T5 embedding space.
- **NumColor-Data:** A 500K synthetic dataset for training color-grounded conditioning.
- **GenColorBench:** A benchmark for evaluating numeric color understanding across ISCC-NBS L1/L3 and CSS3 color naming systems.

## Method

<p align="center">
  <img src="assets/method.png" alt="NumColor Method Overview" width="90%">
</p>

NumColor replaces fragmented color-token embeddings with ColorBook entries **before contextualization** in the T5 text encoder. This allows the color embeddings to flow through self-attention alongside text tokens, binding colors to their target objects without modifying the diffusion backbone.

## Results

<p align="center">
  <img src="assets/results.png" alt="NumColor Qualitative Results" width="90%">
</p>

Quantitative comparison on GenColorBench-Mini (Numeric Color Understanding task):

| Method            | ISCC L1 | ISCC L3 | CSS3  |
|-------------------|:-------:|:-------:|:-----:|
| Qwen-Image        | 25.64   | 18.73   | 14.26 |
| Z-Image           | 22.18   | 16.92   | 12.45 |
| FLUX.2            | 48.72   | 39.29   | 42.67 |
| GPT-Image-1.5     | 51.82   | 48.12   | 49.91 |
| **NumColor + FLUX.1** | **55.71** | **48.02** | **51.96** |

NumColor preserves the base model's pretrained named-color understanding: FLUX.1 achieves 81.27% accuracy on natural color prompts, while NumColor + FLUX.1 attains 80.04% on the same set.

## Release

> 🚧 **Code, pretrained models, and the NumColor-Data / GenColorBench datasets will be released soon.** Please ⭐ this repository to be notified.

Planned releases:

- [ ] Training and inference code
- [ ] Pretrained CTA and ColorBook checkpoints (FLUX.1)
- [ ] NumColor-Data (500K synthetic training set)
- [ ] GenColorBench evaluation suite
- [ ] Project page with interactive demos

## Citation

If you find this work useful, please cite:

```bibtex
@article{butt2026numcolor,
  title={NumColor: Precise Numeric Color Control in Text-to-Image Generation},
  author={Butt, Muhammad Atif and Hernandez, Diego and Gomez-Villa, Alexandra and Wang, Kai and Vazquez-Corral, Javier and Van De Weijer, Joost},
  journal={arXiv preprint arXiv:2603.13547},
  year={2026}
}
```

## Acknowledgements

Computational resources were provided by the Leonardo HPC cluster (CINECA). We are thankful for that.

## Contact

For questions or collaborations, please contact [Muhammad Atif Butt](mailto:mabutt@cvc.uab.es) or open an issue in this repository.

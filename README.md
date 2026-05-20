# Cross-Modal Representational Alignment in Vision and Audio Models

This project investigates whether independently trained vision and audio models develop shared representational structure on semantically paired inputs, and how that alignment compares to vision-language and audio-language alignment. Using layer-wise representational similarity analysis (RSA) and linear predictivity, we examine where and how cross-modal convergence emerges across transformer model architectures.

This is a capstone research project from the Department of Computational Social Science at UC San Diego, under the supervision of Meenakshi Khosla, UC San Diego, Department of Cognitive Science.

---

## Key Findings

- **Vision-audio alignment exists without joint training.** Independently trained vision and audio models show meaningful representational alignment on semantically paired inputs (peak r = 0.295), emerging primarily in mid-to-late layers across all model combinations.
- **Language is the strongest representational bridge.** Vision-language alignment peaked at r = 0.402 and audio-language at r = 0.357, both outperforming direct vision-audio alignment (r = 0.295), positioning language as a stronger cross-modal intermediary than direct perceptual co-occurrence.
- **Audio supervision type matters more than vision model capacity.** BEATs-iter3+ (supervised) consistently outperformed BEATs-iter3 (self-supervised) across all conditions (Δr ≈ +0.055), while DINOv2-large showed only modest, inconsistent advantages over DINOv2-base.
- **Semantically conditioned synthetic images outperform naturalistic frames in early layers.** SDXL-generated images conditioned on AudioCaps captions reached higher alignment earlier than naturalistic middle frames, challenging the assumption that naturalistic stimuli are preferable for alignment studies.

---

## Study Design

**Dataset:** 620 semantically paired audio-image samples from AudioCaps 2.0

**Models:**

| Modality | Model | Params |
|---|---|---|
| Vision | DINOv2-large | 307M |
| Vision | DINOv2-base | 86M |
| Audio | BEATs-iter3+ (supervised) | 90M |
| Audio | BEATs-iter3 (self-supervised) | 90M |
| Language | Qwen3-1.7B | 1.7B |

**Image construction approaches:**
- SDXL-generated images: AudioCaps captions expanded via Phi-3-mini-4k-instruct, then fed to Stable Diffusion XL
- Middle frame extraction: Naturalistic frames extracted from source video files

**Alignment metrics:**
- Representational Similarity Analysis (RSA) using Spearman rank correlation of RDMs
- Linear Predictivity (LP) via ridge regression with 5-fold cross-validation

**Controlled comparisons:**
- Vision model capacity: DINOv2-large vs. DINOv2-base
- Audio supervision type: BEATs-iter3+ vs. BEATs-iter3
- Image type: SDXL-generated vs. naturalistic middle frames
- Three-way modality comparison: vision-audio, vision-language, audio-language

---

## Research Questions

1. Do independently trained vision and audio models show representational alignment on semantically paired inputs, and does alignment follow the early-to-late progression observed in vision-language systems?
2. Is vision-audio alignment stronger or weaker than vision-language and audio-language alignment?
3. Does vision model capacity affect cross-modal alignment?
4. Do audio models trained with labeled data show stronger alignment than self-supervised models?
5. Do SDXL-generated images show greater alignment with audio than naturalistic middle frames?

---

## Limitations

- Dataset limited to 620 samples due to computational constraints from SDXL image generation
- Single language model (Qwen3-1.7B) included; results may vary across model families
- Middle frames manually filtered, which may bias toward naturalistic image representations
- SDXL caption clipping and attribute leakage affected some generated image quality

---

## Authors

Morgan Mahre, Natalie Abel, Alexis Ausland, Yaru Su, Lauren Bolte
UC San Diego, Department of Computational Social Science

Corresponding author: Meenakshi Khosla, UC San Diego, Department of Cognitive Science

---

## References

- Huh et al. (2024). The Platonic Representation Hypothesis. arXiv:2405.07987
- He et al. (2025). Seeing through words, speaking through pixels. EMNLP 2025.
- Wang et al. (2025). Words that make language models perceive. arXiv:2510.02425
- Chen et al. (2023). BEATs: Audio pre-training with acoustic tokenizers. ICML 2023.
- Oquab et al. (2024). DINOv2: Learning robust visual features without supervision.

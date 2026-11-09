# A-CUT MDIQA Teacher Benchmark

> **A-CUT Teacher-Only Performance-Ceiling Benchmark — Official Multi-Dataset IQA (MDIQA) Evaluation on KonIQ-10k, SPAQ, and FLIVE**

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](./LICENSE)
[![Project: A-CUT](https://img.shields.io/badge/Project-A--CUT%20Capstone-success.svg)](https://github.com/gwanjongkim/photo_score_project)

## 1. Overview

- **Role in A-CUT**: Offline Performance-Ceiling Reference & Distillation Teacher (Not for mobile deployment)
- **Task**: Multi-Dataset Transformer No-Reference IQA Benchmark
- **Architecture**: Official Swin-Transformer dual-branch MDIQA teacher (`koniq_seed1`, `koniq_xd`, and unified `net_best` checkpoints) evaluated under the image-only official protocol.

## 2. Input / Output Contract & Model Artifacts

- **Input Contract**: High-resolution RGB images (`384×384` / multi-crop PyTorch pipeline)
- **Output Contract**: Calibrated `[0, 100]` teacher quality score
- **Model Files (`models/model_files/` & Releases)**:
  - `PyTorch teacher-only model (>1 GB checkpoints; not exported to TFLite)`

## 3. Benchmark Results

| Dataset | Official Checkpoint Variant | SRCC | PLCC | RMSE | Status |
| :--- | :---: | :---: | :---: | :---: | :--- |
| **KonIQ-10k** | `koniq_seed1` | **0.9464** | **0.9537** | 4.82 | **Teacher Ceiling** |
| **SPAQ** | `koniq_xd` (Cross-Dataset) | **0.9136** | **0.9173** | 8.41 | **Teacher Ceiling** |
| **FLIVE (Image-Only)** | `net_best` | **0.5692** | **0.6295** | 8.15 | Partial Teacher (Replaced by Prod on FLIVE) |
| **Official 4,967 Combined** | Hybrid MDIQA Teacher | **0.8227** | **0.8490** | - | **Reference Ceiling** |

## 4. Key Engineering Notes & 2026 Audit Findings

- **Checkpoint Source Audit (`results/checkpoint_source_audit_report.md`)**: Verified that `koniq_seed1` (KonIQ SRCC `0.9464`) and `koniq_xd` (SPAQ SRCC `0.9136`) provide near-ceiling supervision, whereas FLIVE requires hybrid fallback because no dedicated FLIVE fusion checkpoint was released upstream.
- **Role in A-CUT**: Used strictly as an offline benchmark ceiling and distillation teacher for `acut-student-iqa`.

## 5. Quick Start

```bash
pip install -r requirements.txt
python scripts/run_mdiqa_official_image_only_benchmark.py --help
python scripts/run_mdiqa_variant_sanity_benchmark.py --help
```

For full documentation, see:
- [`docs/model_card.md`](./docs/model_card.md) — Architecture, tensor contracts, and limitations
- [`docs/benchmark_summary.md`](./docs/benchmark_summary.md) — Detailed metrics and dataset evaluations
- [`docs/reproduction_notes.md`](./docs/reproduction_notes.md) — Environment and reproduction guide
- [`models/download.md`](./models/download.md) — Model binary hashes and download notes

## 6. A-CUT Ecosystem Repositories

| Repository | Dimension | Role / Status | Key Metric |
| :--- | :---: | :--- | :--- |
| [acut-nima-mobile](https://github.com/gwanjongkim/acut-nima-mobile) | Aesthetic (IAA) | **Production Ensemble (0.40)** | AVA SRCC `0.5894`, AUC `0.8018` |
| [acut-rgnet-mobile](https://github.com/gwanjongkim/acut-rgnet-mobile) | Aesthetic (IAA) | **Production Ensemble (0.45)** | AADB SRCC `0.6819` (FP16 `0.6648`) |
| [acut-mobile-alamp](https://github.com/gwanjongkim/acut-mobile-alamp) | Aesthetic (IAA) | **Production Ensemble (0.15)** | AVA Acc `0.7633`, AUC `0.7877` |
| [acut-icaa-color-aesthetics](https://github.com/gwanjongkim/acut-icaa-color-aesthetics) | Color Aesthetics | **Verified TF-Native Port** | ICAA17K Color SRCC `0.8791`, MOS `0.9058` |
| [acut-koniq-flive-technical-iqa](https://github.com/gwanjongkim/acut-koniq-flive-technical-iqa) | Technical (IQA) | **Production Baseline (4/7 + 3/7)** | Official SRCC `0.7168` (`0.7958` recon), `0` Severe FP |
| [acut-technical-iqa](https://github.com/gwanjongkim/acut-technical-iqa) | Technical (IQA) | **Umbrella Benchmark** | 4,967-Image Official Protocol Suite |
| [acut-topiq-mixed112](https://github.com/gwanjongkim/acut-topiq-mixed112) | Technical (IQA) | **Evaluated Candidate** | SPAQ SRCC `0.8990`, KonIQ `0.8630` |
| [acut-topiq-flive-hybrid](https://github.com/gwanjongkim/acut-topiq-flive-hybrid) | Technical (IQA) | **Best Log-Only Shadow (60/40)** | Official SRCC `0.8069`, MAE `5.04` |
| [acut-c6-topiq-koniq](https://github.com/gwanjongkim/acut-c6-topiq-koniq) | Technical (IQA) | **Negative Result (Rejected)** | Official SRCC `0.7314`, MAE `15.39` |
| [acut-mdiqa-benchmark](https://github.com/gwanjongkim/acut-mdiqa-benchmark) | Technical (IQA) | **Teacher Ceiling Reference** | KonIQ SRCC `0.9464`, SPAQ `0.9136` |
| [acut-musiq-probe](https://github.com/gwanjongkim/acut-musiq-probe) | Technical (IQA) | **Reference & Probe Study** | Official SPAQ `0.9460`, KonIQ `0.9275` |
| [acut-student-iqa](https://github.com/gwanjongkim/acut-student-iqa) | Technical (IQA) | **Distillation Study (No-Go)** | 14k Student SRCC `0.7436`, SPAQ `0.8984` |
| [photo_score_project](https://github.com/gwanjongkim/photo_score_project) | Full Monorepo | **Core Research Workspace** | Complete Training, Audit & Pipeline Code |

## 7. References & Citation

- Zhang, W., Zhai, G., Wei, Y., Yang, X., & Ma, K. (2023). *Blind Image Quality Assessment via Vision-Language Correspondence: A Multitask Learning Perspective / Multi-Dataset IQA*. CVPR.

```bibtex
@misc{acut_mdiqa_benchmark_2026,
  title        = {A-CUT MDIQA Teacher Benchmark: A-CUT Teacher-Only Performance-Ceiling Benchmark — Official Multi-Dataset IQA (MDIQA) Evaluation on KonIQ-10k, SPAQ, and FLIVE},
  author       = {Kim, Gwanjung},
  year         = {2026},
  howpublished = {\url{https://github.com/gwanjongkim/acut-mdiqa-benchmark}}
}
```

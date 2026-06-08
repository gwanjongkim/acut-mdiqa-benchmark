# A-CUT MDIQA Benchmark

#### A-CUT Capstone Project — Mobile Image Quality and Aesthetic Assessment

> Evaluation of MDIQA under official protocol.

## Introduction

Evaluation of MDIQA (Multi-Dimensional Image Quality Assessment) under the official protocol. This model serves as a high-performance teacher for technical IQA distillation.

- **Role**: Teacher-only benchmark.
- **Task**: Image Quality and Aesthetic Assessment.

## Model / Method

MDIQA shows state-of-the-art performance on laboratory datasets like KonIQ and SPAQ. However, due to its computational requirements, it is used only as a teacher model and is not intended for mobile production deployment.

- **Artifacts**: Inferred from scripts

## Dataset and Benchmark

- Benchmark results are summarized below. See `docs/benchmark_summary.md` for detailed per-dataset analysis.
- Note: Large datasets are excluded due to size/license constraints.

## Model Weights / Artifacts

- Due to size constraints, artifacts larger than 50MB are not included in this repository.
- Recommended hosting: GitHub Releases.
- See `models/download.md`.

## Repository Structure

```
.
├── configs/
├── docs/
├── models/
├── results/
├── scripts/
└── requirements.txt
```

## Requirements

Please refer to `requirements.txt`. Minimal dependencies include `torch`, `tensorflow`, `numpy`, and `pillow`.

## Quick Start

```bash
pip install -r requirements.txt
python scripts/run_mdiqa_official_image_only_benchmark.py
```
*(Verify path assumptions in `docs/reproduction_notes.md`)*

## Results

| Dataset | Metric | Value | Evidence Path | Decision |
|---------|--------|-------|---------------|----------|
| Official Protocol | MDIQA Selected SRCC | 0.8227 | outputs/official_protocol_mdiqa_signal_benchmark_20260604/report.md | Teacher-Only |
| Official Protocol | MDIQA Selected PLCC | 0.8222 | outputs/official_protocol_mdiqa_signal_benchmark_20260604/report.md | Teacher-Only |
| KonIQ | MDIQA SRCC | 0.9311 | outputs/official_protocol_mdiqa_signal_benchmark_20260604/report.md | Teacher-Only |
| SPAQ | MDIQA SRCC | 0.9136 | outputs/official_protocol_mdiqa_signal_benchmark_20260604/report.md | Teacher-Only |
| FLIVE | MDIQA SRCC | 0.5692 | outputs/official_protocol_mdiqa_signal_benchmark_20260604/report.md | Teacher-Only |

## Limitations

- Results are based on local reproduction and may not exactly match original papers.
- See `docs/model_card.md` for detailed limitations.

## Citation

```bibtex
@misc{acut_mdiqa_2026,
  title        = {A-CUT MDIQA Benchmark: Mobile Image Quality and Aesthetic Assessment Model},
  author       = {Kim, Gwanjung},
  year         = {2026},
  note         = {Capstone project repository}
}
```
### Original References

- Original MDIQA reference will be added after citation verification.

## Related Repositories

- [A-CUT Public Model Repositories](..)

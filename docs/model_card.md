# Model Card — A-CUT MDIQA Teacher Benchmark

## Model Details
- **Model Name**: A-CUT MDIQA Teacher Benchmark (`acut-mdiqa-benchmark`)
- **Developer**: Gwanjung Kim (A-CUT Mobile Photo Evaluation & Curation Capstone)
- **Architecture**: Official Swin-Transformer dual-branch MDIQA teacher (`koniq_seed1`, `koniq_xd`, and unified `net_best` checkpoints) evaluated under the image-only official protocol.
- **Deployment Role**: Offline Performance-Ceiling Reference & Distillation Teacher (Not for mobile deployment)

## Tensor Input / Output Contract
- **Input Contract**: High-resolution RGB images (`384×384` / multi-crop PyTorch pipeline)
- **Output Contract**: Calibrated `[0, 100]` teacher quality score
- **Included Model Artifacts**:
  - `PyTorch teacher-only model (>1 GB checkpoints; not exported to TFLite)`

## Intended Use
- Designed for on-device or offline photo quality and aesthetics evaluation within the A-CUT smartphone photo selection pipeline.
- Not intended as an uncalibrated standalone medical, forensic, or safety-critical classifier.

## Limitations & Audit Qualifications
- **Checkpoint Source Audit (`results/checkpoint_source_audit_report.md`)**: Verified that `koniq_seed1` (KonIQ SRCC `0.9464`) and `koniq_xd` (SPAQ SRCC `0.9136`) provide near-ceiling supervision, whereas FLIVE requires hybrid fallback because no dedicated FLIVE fusion checkpoint was released upstream.
- **Role in A-CUT**: Used strictly as an offline benchmark ceiling and distillation teacher for `acut-student-iqa`.

# Benchmark Summary — A-CUT MDIQA Teacher Benchmark

## Overview
- **Repository**: `acut-mdiqa-benchmark`
- **Role in A-CUT**: Offline Performance-Ceiling Reference & Distillation Teacher (Not for mobile deployment)
- **Task**: Multi-Dataset Transformer No-Reference IQA Benchmark

## Evaluated Metrics

| Dataset | Official Checkpoint Variant | SRCC | PLCC | RMSE | Status |
| :--- | :---: | :---: | :---: | :---: | :--- |
| **KonIQ-10k** | `koniq_seed1` | **0.9464** | **0.9537** | 4.82 | **Teacher Ceiling** |
| **SPAQ** | `koniq_xd` (Cross-Dataset) | **0.9136** | **0.9173** | 8.41 | **Teacher Ceiling** |
| **FLIVE (Image-Only)** | `net_best` | **0.5692** | **0.6295** | 8.15 | Partial Teacher (Replaced by Prod on FLIVE) |
| **Official 4,967 Combined** | Hybrid MDIQA Teacher | **0.8227** | **0.8490** | - | **Reference Ceiling** |

## Key Engineering & Audit Findings

- **Checkpoint Source Audit (`results/checkpoint_source_audit_report.md`)**: Verified that `koniq_seed1` (KonIQ SRCC `0.9464`) and `koniq_xd` (SPAQ SRCC `0.9136`) provide near-ceiling supervision, whereas FLIVE requires hybrid fallback because no dedicated FLIVE fusion checkpoint was released upstream.
- **Role in A-CUT**: Used strictly as an offline benchmark ceiling and distillation teacher for `acut-student-iqa`.

## Evidence Files in `results/`
All metric tables, per-sample predictions, parity checks, and audit reports backing the numbers above are stored directly in the [`results/`](../results/) directory of this repository.

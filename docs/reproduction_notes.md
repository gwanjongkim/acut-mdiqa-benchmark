# Reproduction & Execution Notes — A-CUT MDIQA Teacher Benchmark

## Environment Setup
```bash
python3 -m venv .venv
source .venv/bin/activate
pip install --upgrade pip
pip install -r requirements.txt
```

## Available Scripts (`scripts/`)
```bash
python scripts/run_mdiqa_official_image_only_benchmark.py --help
python scripts/run_mdiqa_variant_sanity_benchmark.py --help
```

## Preprocessing & Parity Verification
- **Input Specification**: High-resolution RGB images (`384×384` / multi-crop PyTorch pipeline)
- **Output Specification**: Calibrated `[0, 100]` teacher quality score
- Ensure EXIF orientation transposition (`ImageOps.exif_transpose`) is applied prior to resizing so portrait smartphone photos are not evaluated rotated.

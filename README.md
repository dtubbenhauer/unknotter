# Uncrossing number / RL unknotting (notebook)

This repository contains a Jupyter notebook (`notebooks/uncrossing.ipynb`) for training / evaluating an RL agent for simplifying “hard” unknot diagrams, including utilities for exporting **KnotInfo-compatible Jones vectors** and matching them up to mirror + shift.

## What’s in here
- **Notebook**: `notebooks/uncrossing.ipynb` (narrative + experiments)
- **Reproducibility knobs**: configurable paths via environment variables (see below)
- **External file**: that you can run in google colab if you have problems (it wants you to have files saved in google drive)

## Install (local)
```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

> Note: `stable-baselines3` will pull in `torch`. If you want GPU, install an appropriate PyTorch build first (then install `stable-baselines3`).

## Run (local)
```bash
jupyter lab
# open notebooks/uncrossing.ipynb and Run All
```

The notebook is **local-first**: by default it treats the current working directory as `PROJECT_DIR` and expects files under:
- `./data/`  (inputs)
- `./outputs/` (models/logs/results)

Create these folders (or let the notebook create `outputs/` automatically).

### Environment variables (optional)
You can override paths without editing the notebook:

- `PROJECT_DIR` (default: `pwd`)
- `DATA_DIR` (default: `${PROJECT_DIR}/data`)
- `OUT_DIR`  (default: `${PROJECT_DIR}/outputs`)
- `PD_PATH` (default: `${DATA_DIR}/3-16.txt`)
- `SMALL_JONES` (default: `${DATA_DIR}/small-jones.txt`)
- `BEST_MODEL_PATH` (default: `${OUT_DIR}/best_model.zip`)
- `TB_DIR` (default: `${OUT_DIR}/tb`)

Example:
```bash
export PROJECT_DIR="$HOME/uncrossing-number"
export OUT_DIR="$PROJECT_DIR/outputs_run1"
```

## Run on Colab (optional)
If you prefer Colab + Drive, set:
```python
import os
os.environ["USE_COLAB_DRIVE"] = "1"
```
and (optionally) set `PROJECT_DIR` to your Drive folder.

## GCS input
The notebook includes helpers to read the **first column** from CSV files stored on GCS via `gcsfs`.

You can override the paths with env vars, e.g.
```bash
export GCS_CSV_PATH_MAIN="gs://your-bucket/hard_unknots.csv"
```

For local runs, you’ll need Google credentials available to `gcsfs` (ADC, service account JSON, etc.). If you don’t want GCS, just point the notebook at local files instead.

## Keeping notebook diffs clean
Recommended:
- clear outputs before committing, or
- install `nbstripout`:
  ```bash
  pip install nbstripout
  nbstripout --install
  ```

## License
Unlicensed.

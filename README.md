# Uncrossing number / RL unknotting (notebook)

This repository contains a Jupyter notebook (`notebooks/uncrossing.ipynb`) for training / evaluating an RL agent for simplifying “hard” unknot diagrams, including utilities for exporting **KnotInfo-compatible Jones vectors** and matching them up to mirror + shift.

## What’s in here
- **Notebook**: `notebooks/uncrossing.ipynb` (narrative + experiments)
- **Reproducibility knobs**: configurable paths via environment variables (see below)
- **External file**: uncrossing.ipynb that you can run in google colab if you have problems (it wants you to have files saved in google drive)
- **Hard unknots**: If you are interested in the hard unknots and their unknotting, use hard_unknot.ipynb that you can run in google colab if you have problems (it wants you to have files saved in google drive)

## Install (local)
```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

> Note: `stable-baselines3` will pull in `torch`. If you want GPU, install an appropriate PyTorch build first (then install `stable-baselines3`).

You also need to unzip the file knotinfo_data_complete.zip in the folder you have found it.

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
This is free and unencumbered software released into the public domain.

Anyone is free to copy, modify, publish, use, compile, sell, or
distribute this software, either in source code form or as a compiled
binary, for any purpose, commercial or non-commercial, and by any
means.

In jurisdictions that recognize copyright laws, the author or authors
of this software dedicate any and all copyright interest in the
software to the public domain. We make this dedication for the benefit
of the public at large and to the detriment of our heirs and
successors. We intend this dedication to be an overt act of
relinquishment in perpetuity of all present and future rights to this
software under copyright law.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS BE LIABLE FOR ANY CLAIM, DAMAGES OR
OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE,
ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR
OTHER DEALINGS IN THE SOFTWARE.

For more information, please refer to <https://unlicense.org>

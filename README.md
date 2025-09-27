# Dodgeball Analytics: Player Detection → Throw Categorization → Ball Counts → Win-Rate & Impact

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1OZbOTxo16YGmxt-V08jD19TMM3QxdOfn)

This repository contains a reproducible pipeline to:

- Extract player/throw coordinates from match video using YOLOv8 and court homographies
- Categorize throws (Phase-1 logic) and tag events with context (e.g., opening_rush, set_throw, counter_rush, dump, bounce)
- Analyze success rates by throw type, including punish/follow-up effects
- Estimate ball counts over time with anchor logic and rollback suggestions for QA
- Predict win rate and compute per-category impact metrics

Best way to run: open the notebooks in Google Colab using the badge above. The notebooks were written and tested for Colab with Google Drive as the backing store.

All example match videos referenced by this work can be found on the NSWDL YouTube channel.

---

### What each notebook does

1) **Complete_Workflow_Generating_Coordinates.ipynb**  
   - Mounts Google Drive and loads input spreadsheets (events and court corners) plus a video  
   - Runs YOLOv8 person detection and maps detections to a canonical top-down court via homographies  
   - Produces per-throw rectified coordinates and small court visualizations

2) **Throw_type_categorization_full_workflow.ipynb**  
   - Applies time data and coordinates data to label throws (opening_rush, set_throw, counter_rush, dump, bounce, ties, etc.)  
   - Adds punish and follow-up flags; exports per-throw/category tables

3) **Ball_Count_Tracking.ipynb**  
   - Estimates ball_t0/ball_t1 sequences using anchors (set_throw-based targets), with rollback suggestions for QA  
   - Exports a full events file with color-coded rows and a review file

4) **xgb_win_rate_prediction.ipynb**  
   - Trains/evaluates a model (e.g., XGBoost) to estimate win rate and impact by throw type and situation  
   - Outputs summary tables and plots

---

## Quick start (Colab)

1. Click the “Open in Colab” badge at the top.  
2. In Colab: Runtime → Change runtime type → select GPU T4 (recommended for YOLO).  
3. Run the first setup cell to install dependencies and mount Google Drive.  
4. Keep default paths or update to your own Drive folders.  
5. Execute cells in order.

---

## Requirements (local option)

Running in Colab requires no local setup. If you prefer local execution:

- Python 3.10+  
- Packages: `ultralytics==8.2.0`, `opencv-python`, `torch` (CUDA build recommended), `pandas`, `numpy`, `matplotlib`, `openpyxl`, `tqdm`, `xgboost`  
- NVIDIA GPU and CUDA for reasonable inference speed

Note: If using newer PyTorch versions, see the notebook cells that add `torch.serialization.add_safe_globals(...)` or pin to a known-working version.

---

## Data and videos

- Videos are not stored in this repository. Use your own videos or public NSWDL YouTube uploads.  
- Input spreadsheets (events and court coordinates) are read from Google Drive or downloaded in-notebook.  
- Outputs (coordinates, categorized throws, ball counts, figures) are written back to Drive.

If you need to version large artifacts in Git, use Git LFS. Otherwise, keep this repository code-only and rely on Drive/Colab for data.

---

## Reproducibility

- Given the same inputs and versions, notebooks are deterministic.  
- Dependencies are pinned where appropriate; Colab is the recommended environment.  
- Changing YOLO weights or thresholds will affect outputs.

---

## Citation

If you use this code in academic work, please cite your paper and this repository.  
Acknowledgment: NSWDL for public match footage used in examples.

---


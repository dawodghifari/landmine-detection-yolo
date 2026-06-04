# Landmine Detection from Drone Thermal Imagery (YOLOv11)

Real-time antipersonnel landmine detector trained on UAV **thermal (RJPEG) imagery** using the lightweight YOLO11n architecture — detecting buried "legbreaker" mines at 0–10 cm depths.

![Sample predictions](assets/sample_predictions.jpg)

## Pipeline

1. **Data curation** — filtered a raw corpus of 2,700 multisource images (JPEG/RJPEG/TIFF, mine + free-zone scenes) down to 465 valid RJPEG frames containing buried mines; split 314 train / 80 val / 71 test with YOLO-format annotations.
2. **Training** — YOLO11n fine-tuned for 50 epochs at 640px (Apple MPS backend).
3. **Evaluation** — quantitative validation (PR curves, confusion matrix), qualitative inference, and **negative-image validation** against mine-free scenes to measure false-positive behaviour.

## Results (test set)

| Metric | Value |
|---|---|
| mAP@50 | **0.68** |
| Precision | 0.71 |
| Recall | 0.66 |

| | |
|---|---|
| ![Training metrics](assets/train_metrics.png) | ![PR curve](assets/PR_curve.png) |

## Repo contents

| Path | Description |
|---|---|
| `notebooks/landmine.ipynb` | Full pipeline: data prep → training → evaluation |
| `landmine.yaml` | YOLO dataset config (point at your local dataset copy) |
| `training/results.csv` | Per-epoch training log |
| `docs/ELEC3612_Project_2_Report.pdf` | 14-page report with full methodology |

**Dataset:** UAV thermal imagery of buried landmines, from a published *Data in Brief* dataset (multi-flight, multi-altitude, labelled by mine location and burial depth). Not redistributed here — see the report for the citation and source.

## Run it

```bash
pip install -r requirements.txt
# download the dataset (see docs/report), update paths in landmine.yaml, then:
jupyter notebook notebooks/landmine.ipynb
```

## Context

Pattern Recognition & Machine Intelligence project (ELEC3612, University of Sydney, 2025 — course mark: 89 HD). Solo work.

# Computer Vision Projects

<div align="center">

![Python](https://img.shields.io/badge/Python-3.10-blue?style=for-the-badge&logo=python)
![YOLOv8](https://img.shields.io/badge/YOLOv8m-Ultralytics-purple?style=for-the-badge)
![Streamlit](https://img.shields.io/badge/Streamlit-Apps-red?style=for-the-badge&logo=streamlit)
![Docker](https://img.shields.io/badge/Docker-Compose-2496ED?style=for-the-badge&logo=docker)

A collection of end-to-end computer vision systems — from dataset curation through training to deployed applications. Each project below lives in this repo as a **git submodule** with its own full history, README, and codebase.

</div>

---

## Table of Contents

- [Projects](#projects)
  - [BD License Plate Detector](#1-bd-license-plate-detector)
  - [Fabric Defect Detector](#2-fabric-defect-detector)
- [Cloning This Repo](#cloning-this-repo)
- [Author](#author)

---

## Projects

### 1. [BD License Plate Detector](https://github.com/rahhhmann/BD-License-Plate-Detector)

An end-to-end Bangladeshi vehicle & license plate detection, tracking, and OCR pipeline, deployed as a multi-page Streamlit app.

**Highlights:**
- Two-stage YOLOv8m plate detector + a custom YOLOv8m character-detector ("chardet") for Bangla OCR — chosen over TrOCR/EasyOCR after benchmarking (chardet: 0.026 avg CER, 79.4% exact-match on the test split)
- Pipeline includes same-class IoU deduplication (fixes duplicate-character OCR bug), lightweight BRTA-format plausibility validation, and confidence-tiered bounding boxes (green/amber/red) tied to a weakest-link `overall_confidence` score
- Expanded scope ("BD Traffic Vision"): a BNVD-trained YOLOv8m vehicle detector (car/bus/motorcycle/CNG) — mAP50 0.925, mAP50-95 0.685, ~33.7 FPS — associated with plate detections via center-point containment
- Supports both image and video modes; video mode uses ByteTrack for persistent vehicle track IDs
- Dedicated "Traffic Detection" page handles wide multi-vehicle traffic photos by detecting vehicles first, then running the plate pipeline per cropped vehicle
- Deployed on Streamlit Community Cloud: **[bd-number-plate-detection.streamlit.app](https://bd-number-plate-detection.streamlit.app/)**

**Stack:** YOLOv8m, Ultralytics, ByteTrack, Streamlit, Kaggle T4 GPU training

---

### 2. [Fabric Defect Detector](https://github.com/rahhhmann/Fabric-Defect-Detector)

An automated fabric defect detection system for Bangladesh's RMG (garment) industry, built to address slow, inconsistent manual QC inspection.

**Highlights:**
- YOLOv8m detector for 5 defect classes: Stain, Thread, Warp/Weft, Hole, Seam
- Two training runs — v2 applied targeted oversampling for the underrepresented Seam class, improving mAP50 from **0.7891 → 0.8425**
- Production-style FastAPI backend with three endpoints (`/predict`, `/predict/annotated`, `/predict/batch`) plus an interactive Streamlit QC dashboard
- Fully Dockerized (`docker-compose up --build` runs the whole platform) and deployed on Render as separate API and dashboard services
- Trained on Kaggle T4 GPU using a Roboflow Universe dataset

**Stack:** YOLOv8m, FastAPI, Streamlit, Docker Compose, Render, Kaggle T4 GPU

---

## Cloning This Repo

Since the projects above are submodules, clone with `--recurse-submodules` to pull their contents too:

```bash
git clone --recurse-submodules https://github.com/rahhhmann/Computer-Vision.git
```

If you already cloned without that flag:

```bash
git submodule update --init --recursive
```

To pull the latest changes from each submodule's upstream repo:

```bash
git submodule update --remote --merge
```

---

## Author

**Ashikur Rahman**
CSE, Patuakhali Science and Technology University (PSTU)
GitHub: [rahhhmann](https://github.com/rahhhmann) · HuggingFace: [ashik297](https://huggingface.co/ashik297) · Kaggle: [singertv](https://www.kaggle.com/singertv)

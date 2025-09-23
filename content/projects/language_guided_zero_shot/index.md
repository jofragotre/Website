---
title: "Language‑Guided Zero‑Shot Object Detection"
summary: "YOLO + CLIP pipeline that detects objects guided by natural‑language prompts (webcam demo included)."
tags: ["Zero‑Shot", "VLM", "CLIP", "YOLO", "SAM", "Computer Vision"]
thumbnail: "cover.png"
cover: "cover.png"   # optional: add a screenshot from the webcam demo
weight: 2
showToc: false
---

A simple, practical pipeline for **zero‑shot object detection** using **YOLO** for detections and **CLIP** for language guidance. Provide natural‑language prompts (e.g., “a black smartphone”), and the system highlights the best‑matching object in images or live webcam. Under improvement! 

# Implementation details

{{< button href="https://github.com/jofragotre/Language-Guided-Zero-Shot-Object-Detection" >}}
Code on GitHub
{{< /button >}}

## Features
- Zero‑shot detection without task‑specific training
- Language‑guided selection with **CLIP** (image–text similarity)
- **YOLO** for detection/segmentation; optional **SAM** prototype
- Customizable prompts
- Webcam demo for real‑time testing

## Project structure
- `segmentation/`
  - `yolo_detection.py` — YOLO‑based object detection
  - `sam_detection.py` — SAM‑based detection (prototype)
- `selector.py` — CLIP‑based selection of detections by prompt similarity
- `models/` — pre‑trained model weights (YOLO, CLIP)
- `resources/` — sample images
- `README.md` — documentation

## Requirements
- Python 3.8+
- PyTorch
- OpenCV
- Ultralytics (YOLO, SAM)
- OpenAI CLIP (`clip`)

Install (example):
```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

## Usage

Webcam demo:
```bash
python segmentation/webcam_demo.py
```

Customize prompts in `webcam_demo.py`:
```python
self.object_prompt = [
    "A black smartphone",
    "A person wearing a red shirt",
    "A remote controller",
    "A frying pan",
]
```

The demo:
- runs YOLO to detect objects
- crops detections
- ranks crops by CLIP similarity to your prompts
- overlays boxes + matched prompt on the live feed

## Example
Given the prompt “A black smartphone”:
1) YOLO finds candidate objects  
2) Each crop is embedded with CLIP  
3) Text–image similarity is computed for the prompt  
4) The highest‑scoring object is highlighted

## Notes / roadmap
- Add lightweight **Ultralytics SAM** acceleration for live use
- Implement **NMS** consolidation across overlapping detections
- Consider detection models with broader class sets or custom training
- Package a simple executable for non‑dev users

## Troubleshooting
- File/path errors → run scripts from repo root; check relative paths
- Close similarity scores → refine prompts; ensure consistent preprocessing
- Model downloads → verify internet/SSL; confirm cache directory
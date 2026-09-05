# Crack Detection with YOLO26

[![Open training notebook in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Farhana-Tani/training-and-testing-yolo26-instance-segmentation/blob/main/Training_Yolo26_Instance_Segmentation.ipynb)
[![Open testing notebook in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Farhana-Tani/training-and-testing-yolo26-instance-segmentation/blob/main/Testing_Yolo26_Instance_Segmentation.ipynb)

Train and test a YOLO26 instance-segmentation model for identifying cracks in surface images. The notebooks use Ultralytics YOLO to predict both object locations and pixel-level masks, making the project useful for visual inspection workflows involving concrete, walls, and related surfaces.

> This project is an experimental computer-vision workflow. Its predictions do not replace inspection or assessment by qualified professionals.

## Overview

Unlike bounding-box-only detection, **instance segmentation** outlines each predicted crack with a mask. This repository contains two Google Colab-ready notebooks:

- [`Training_Yolo26_Instance_Segmentation.ipynb`](Training_Yolo26_Instance_Segmentation.ipynb) downloads/prepares a YOLO-format crack dataset and trains a segmentation model.
- [`Testing_Yolo26_Instance_Segmentation.ipynb`](Testing_Yolo26_Instance_Segmentation.ipynb) loads trained weights and demonstrates inference on a single image, a batch of images, and an OpenCV/NumPy image array. It also shows how to combine predicted crack masks for visualization.

## Highlights

- YOLO26 instance segmentation through the Ultralytics Python package.
- Crack dataset referenced from [Roboflow Universe](https://universe.roboflow.com/university-bswxt/crack-bphdr).
- Google Colab-friendly training and testing workflows.
- Inference examples for image files, batches, and NumPy arrays.
- Saved visual outputs and an example of extracting class-specific masks.

## Pipeline

```text
Crack images + polygon annotations
              ↓
YOLO-format dataset (`data.yaml`)
              ↓
Fine-tune YOLO26 segmentation model
              ↓
Trained weights (`best.pt` / `last.pt`)
              ↓
Prediction: boxes, classes, confidence scores, and masks
```


## Local Installation

```bash
git clone https://github.com/Farhana-Tani/training-and-testing-yolo26-instance-segmentation.git
cd training-and-testing-yolo26-instance-segmentation

python -m venv .venv
# macOS/Linux
source .venv/bin/activate
# Windows PowerShell
# .venv\\Scripts\\Activate.ps1

pip install ultralytics opencv-python matplotlib torch
```

> **Note:** This is a notebook-based repository and it does not currently include a `requirements.txt`. Pin package versions in one for reproducible local runs.

## Dataset Setup

The training notebook expects a YOLO-format dataset archive named `crack.v2i.yolo26.zip`, extracts it to `dataset/`, and reads its `data.yaml` file.

```bash
# In Colab, after placing the archive in /content:
unzip /content/crack.v2i.yolo26.zip -d /content/dataset
```

```text
dataset/
├── data.yaml
├── train/
│   ├── images/
│   └── labels/
├── valid/
│   ├── images/
│   └── labels/
└── test/                   # if included in the dataset export
    ├── images/
    └── labels/
```


## Repository Structure

```text
.
├── Training_Yolo26_Instance_Segmentation.ipynb  # Dataset setup and model training
├── Testing_Yolo26_Instance_Segmentation.ipynb   # Inference and mask visualization
├── LICENSE                                      # MIT License
└── README.md
```

## Evaluation Guidance

Evaluate on held-out images that were not used to train or tune the model. Useful checks include:

- box and mask precision/recall;
- segmentation and detection mAP at documented IoU thresholds;
- visual review of missed cracks and false positives;
- robustness across lighting, texture, camera distance, shadows, joints, and stains.

Document the dataset split, model weights, confidence threshold, and evaluation command alongside any reported metric.



## License

This repository is released under the [MIT License](LICENSE).

## Acknowledgments

- [Ultralytics](https://docs.ultralytics.com/) for the YOLO framework.
- [Roboflow Universe](https://universe.roboflow.com/) for the referenced dataset hosting and workflow.

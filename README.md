# Smart Agricultural Weed Management System

This repository contains the official code and resources for the research presented in the following papers:

1. **"Quantized YOLO for Real-Time Weed Detection: An Affordable Embedded System for Precision Agriculture"**  
   *Proceedings of SBIAGRO 2025*

2. **"Real-Time Weed Detection on Low-Cost Embedded Devices Using Quantized YOLO"**  
   *2025 16th IEEE International Conference on Industry Applications (INDUSCON)*

## Abstract

This research addresses challenges in precision agriculture through the development of an affordable embedded system for real-time weed detection. By applying advanced deep learning optimization techniques to YOLOv5 neural networks deployed on edge computing platforms, we demonstrate how agricultural computer vision can be made accessible for producers of all sizes. Our methodology combines post-training quantization (16-bit floating point, 8-bit integer) and ONNX format conversion with systematic performance benchmarking on the Raspberry Pi 4B platform.

## Key Features

- **Affordable Hardware**: Designed for Raspberry Pi 4B (~$60), democratizing precision agriculture.
- **Deep Learning Optimization**: Utilizes Quantization (FP16, INT8) and ONNX for real-time performance.
- **Agricultural Relevance**: Trained on the 4Weed Dataset covering Cocklebur, Foxtail, Redroot Pigweed, and Giant Ragweed.
- **Real-Time Performance**: Achieves up to 2.66 FPS (ONNX) on RPi 4B, suitable for tractor speeds up to 10 km/h.

## Methodology

### Dataset
We used the [4Weed Dataset](https://osf.io/w9v3j/overview) containing 618 images of four weed species:
1. **Cocklebur** (*Xanthium Strumarium*)
2. **Foxtail** (*Setaria Viridis*)
3. **Redroot Pigweed** (*Amaranthus Retroflexus*)
4. **Giant Ragweed** (*Ambrosia Trifida*)

The dataset was split into training (518) and validation (100) sets.

### YOLOv5 Architecture
We explored YOLOv5n, s, m, l, and x models. Training was conducted at 640x640 resolution for 150 epochs.

### Optimization Techniques
1. **FP16**: 16-bit floating point quantization.
2. **INT8**: 8-bit integer quantization (Post-Training Quantization).
3. **ONNX**: Open Neural Network Exchange format.

## Results

### Accuracy (mAP@0.5) vs Speed (FPS) on Raspberry Pi 4B

| Model | Format | mAP@0.5 | FPS | Inference (s) |
|-------|--------|---------|-----|---------------|
| **YOLOv5n** | **ONNX** | 0.727 | **2.66** | 0.376 |
| YOLOv5s | ONNX | 0.785 | 1.15 | 0.869 |
| **YOLOv5l** | **INT8** | **0.815** | 0.18 | 5.685 |

**Conclusion**:
- **YOLOv5n-ONNX** is best for real-time mobile applications (spraying at ~10 km/h).
- **YOLOv5l-INT8** is best for high-accuracy stationary analysis.

## Getting Started

### Prerequisites
- Python 3.8+
- [Git](https://git-scm.com/)

### Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/LuizCMarquesJr/Smart-Agricultural-Weed-Management-Real-Time-Detection-System-Using-Quantized-YOLO.git
   cd Smart-Agricultural-Weed-Management-Real-Time-Detection-System-Using-Quantized-YOLO
   ```

2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

3. (Optional) Clone YOLOv5 submodule if you plan to retrain:
   ```bash
   git clone https://github.com/ultralytics/yolov5
   cd yolov5
   pip install -r requirements.txt
   cd ..
   ```

## Usage

### 1. Dataset Preparation
Run the dataset preparation notebook to download the 4Weed dataset and organize it for YOLOv5:
- `notebooks/01_Dataset_Preparation.ipynb`

### 2. Training
To reproduce the training results:
- `notebooks/02_YOLOv5_Training.ipynb`

### 3. Quantization & Export
To convert trained models to ONNX and apply quantization:
- `notebooks/03_Quantization_and_Export.ipynb`

## Citation
If you use this work, please cite our papers:

### SBIAGRO 2025
```bibtex
@article{marques2025quantized,
  title={Quantized YOLO for Real-Time Weed Detection: An Affordable Embedded System for Precision Agriculture},
  author={Marques Jr, L. C. and Papa, J. P. and Ulson, J. A. C.},
  journal={Proceedings of SBIAGRO},
  year={2025}
}
```

### IEEE INDUSCON 2025
```bibtex
@inproceedings{marques2025realtime,
  title={Real-Time Weed Detection on Low-Cost Embedded Devices Using Quantized YOLO},
  author={Marques Jr, L. C. and Ulson, J. A. C.},
  booktitle={2025 16th IEEE International Conference on Industry Applications (INDUSCON)},
  pages={1--6},
  year={2025},
  organization={IEEE},
  doi={10.1109/INDUSCON66435.2025.11241472}
}
```

## License
This project is licensed under the GPL-3.0 License.

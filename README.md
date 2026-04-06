# fathomnet2025
FathomNet 2025 (CVPR-FGVC) is a vision challenge for hierarchical marine species classification. Models must navigate a 79-category biological tree, scored by the "Hierarchical Distance" from ground truth. It tests domain adaptation, as models train on shallow-water data but must generalize to deep-sea imagery with unique lighting and haze.


---

# 🌊 FathomNet 2025: Marine Life Image Classification & Detection

This repository contains the implementation of a dual-technique approach for the **FathomNet 2023 Out-of-Distribution Challenge**. We combine the robust feature extraction of **ResNet50** for classification with the real-time detection capabilities of **YOLOv8** to identify and localize marine organisms in high-resolution deep-sea imagery.

## 🚀 The Challenge
Marine life identification faces significant "Out-of-Distribution" (OOD) challenges due to varying lighting, depths, and rare species. Our solution focuses on:
* **Data Bottleneck Resolution:** Moving from 20GB+ of raw high-res images to focused Region of Interest (ROI) crops.
* **Scale Variance:** Using localized crops to ensure small organisms are not lost in high-resolution backgrounds.

---

## 🛠️ Tech Stack & Architectures

### 1. ResNet50 (Classification Backbone)
We utilize a **ResNet50** model pre-trained on ImageNet-1K, fine-tuned specifically on 23,699 localized crops from the FathomNet training set.
* **Input:** 224x224 ROI Crops.
* **Optimization:** Adam Optimizer ($lr=1e-4$) with Cross-Entropy Loss.
* **Purpose:** High-accuracy classification of the 79 biological categories.

### 2. YOLOv8 (Detection & Localization)
To handle the "Detection" aspect of the competition, we implement **YOLOv8** (You Only Look Once v8).
* **Function:** Simultaneous bounding box regression and class prediction.
* **Benefit:** Superior performance in identifying multiple organisms within a single frame.

---

## 📂 Project Structure

```bash
├── data/
│   ├── dataset_train.json       # COCO-formatted metadata
│   ├── train_rois_final/        # 23,699 localized crops ({img_id}_{ann_id}.png)
│   └── train_data_sorted/       # Sorted sub-folders by Category ID
├── scripts/
│   ├── download_and_crop.py     # Async downloader & ROI extractor
│   ├── sort_classes.py          # Taxonomic folder organization
│   ├── train_resnet.py          # ResNet50 training pipeline
│   └── train_yolo.py            # YOLOv8 training & inference
├── models/
│   └── resnet50_v1.pth          # Saved model weights
└── README.md
```

---

## 📉 Methodology & Pipeline

### Phase 1: Data Engineering
Raw images are processed asynchronously using `httpx` and `PIL`. Instead of loading 20GB into memory, we extract specific **Regions of Interest (ROI)** based on annotation coordinates. These crops are then zipped and moved to a local SSD to eliminate Google Drive I/O latency.



### Phase 2: Classification (ResNet)
The dataset is split 80/20 into training and validation sets. We apply heavy data augmentation (Horizontal Flips, Normalization) to improve the model's robustness against OOD marine environments.

### Phase 3: Detection (YOLO)
YOLOv8 is trained on the full-frame images to learn spatial context, allowing the model to distinguish between organisms and complex seabed backgrounds.

---

## 📊 Results (Build A)
* **Dataset Size:** 23,699 Annotations.
* **Hardware:** NVIDIA T4 GPU (Google Colab).
* **Training Time:** ~1.5 hours (15 Epochs).
* **Base Score Improvement:** Targeted > 5.67 (Challenge Baseline).

---

## 🛠️ How to Run

1.  **Clone the Repo:**
    ```bash
    git clone https://github.com/yourusername/fathomnet-resnet-yolo.git
    ```
2.  **Install Dependencies:**
    ```bash
    pip install torch torchvision ultralytics tqdm httpx nest-asyncio
    ```
3.  **Run the Pipeline:**
    * Execute `download_and_crop.py` to build the ROI library.
    * Execute `sort_classes.py` to organize data by taxonomy.
    * Run `train_resnet.py` to begin training.

---

## 📜 License
Distributed under the MIT License. See `LICENSE` for more information.

**Author:** Ikan Laut Group
**Location:** Malaysia  
**Build Version:** Build A
# FathomNet 2025: Hierarchical Marine Species Classification

**Team Name:** Ikan Laut
**Kaggle Ranking:** 11th Place
**Best Public Score:** 2.53
**Track:** 1 — Kaggle Competition (CVPR-FGVC 2025)

## 🌊 Project Overview

This repository contains the deep learning pipeline developed by team **Ikan Laut** for the FathomNet 2025 competition. The objective is to automate the classification of ocean life using hierarchical labels. Marine imagery is uniquely difficult to work with — haze, low light, occlusion, and a long-tailed species distribution all make this a hard fine-grained classification problem.

We explored four families of architectures (ResNet-50, ConvNeXt, YOLOv8, and Swin-B) before converging on a **Swin Transformer-Base (Swin-B)** pipeline, optimized with dynamic class weighting, label smoothing, and an aggressive data I/O strategy to keep GPU utilization high.

## 👥 The Team (Ikan Laut)

| Member | Primary Responsibility | Key Focus |
| :--- | :--- | :--- |
| **Nazhan** | ResNet User | ResNet-50 Optimization & ConvNeXt Experiments |
| **Akmal** | Detection Researcher | YOLOv8 Implementation & Localization |
| **Adibah** | Transformer Lead | Swin-B Architecture & Attention Mechanisms |

## 📈 Experimental Journey & Results

We progressed from standard CNN baselines to a high-performing Swin-B pipeline, incorporating local attention mechanisms and rigorous optimization techniques along the way.

| Iteration | Architecture | Key Technique | Public Score | Status |
| :--- | :--- | :--- | :--- | :--- |
| 1 | ResNet-50 | Baseline | 3.45 | Baseline |
| 2 | ViT-B/16 | None | 2.92 | Experimental |
| 3 | Swin-B | Default (224x224) | 2.68 | Logged |
| 4 | **Swin-B** | **Dynamic Weights + Smoothing** | **2.53** | **Final** |

A separate detection-first track was also explored with YOLOv8:

| Experiment | Model Architecture | Resolution | Technique / Strategy | Public Score |
| :--- | :--- | :--- | :--- | :--- |
| 01 (Baseline) | YOLOv8m (Detection) | 640px | Single-stage detection baseline | 7.26 |
| 02 (Specialist) | YOLOv8m-cls | 224px | Two-stage pipeline with ROI extraction | 3.77 |
| 03 (HD Detail) | YOLOv8l-cls | 448px | High-res, fine-grained taxonomic features | 3.82 |
| 04 (Ensemble) | Medium + Large | Mixed | Weighted averaging (0.7M / 0.3L) | **3.60** |

> Lower score = better (hierarchical distance metric).

## 🛠️ Technical Strategy

* **Swin-B Architecture:** Shifted-window self-attention captures localized marine organism details, outperforming flat global-attention models. The standard classification head was replaced with a custom linear layer mapping latent features to taxonomic categories.
* **Preprocessing & I/O:** To eliminate latency, images were downloaded and cropped to Regions of Interest (ROIs), then migrated from Google Drive to high-speed local Colab SSD storage. Metadata (annotations, category IDs) was parsed on-the-fly for streamlined PyTorch `ImageFolder` loading.
* **Optimization Rigor:**
  * **Imbalance Handling:** Dynamic class weighting in `nn.CrossEntropyLoss`, based on inverse directory frequencies, to counter the long-tailed species distribution.
  * **Regularization:** 0.1 label smoothing to combat noisy/ambiguous annotations.
  * **Training Dynamics:** AdamW (weight decay 0.01–0.05) with a OneCycleLR or CosineAnnealingLR schedule, peak learning rates in the 4e-4 to 5e-5 range depending on the architecture.

## 📂 Directory Structure

```
fathomnet2025/
├── models/
│   ├── YoloV8/        # Detection-based pipeline (Akmal)
│   ├── Swin-B/         # Final winning architecture (Adibah)
│   ├── Resnet/         # ResNet-50 "Build A" baseline (Nazhan)
│   └── ConvNeXT/       # ConvNeXt experimental pivot (Nazhan)
├── submission/         # Final, replicable Swin-B submission pipeline
├── prep/                # Dataset download & ROI cropping utilities
├── results/             # Leaderboard screenshots, submission proofs, comparisons
└── requirements.txt
```

* **`models/`** — One folder per architecture explored, each with an `explanation.md` (what the model is and why we used it), a `procedure.md` (step-by-step training pipeline), and the corresponding training script/notebook.
* **`submission/`** — Standalone, reproducible version of the final Swin-B model with setup instructions (`read.md`) for both Colab and local execution.
* **`prep/`** — Async download + bounding-box cropping scripts (`download_images.py`) used to turn raw FathomNet imagery into classification-ready ROI crops.
* **`results/`** — Leaderboard screenshot, submission screenshots, and `model_comparison.md` (a deeper architecture trade-off analysis across ResNet, ConvNeXt, Swin, and YOLOv8).

## 🧠 Model Breakdown

### Swin Transformer-Base (Final Model)
Hierarchical, shifted-window attention (`microsoft/swin-base-patch4-window7-224` / `torchvision.models.swin_b`). Best at resolving fine-grained, regional species detail under varying object scale. More GPU/VRAM-hungry and data-hungry than CNNs, but ultimately delivered the best score after adding dynamic class weighting and label smoothing. See `models/Swin-B/`.

### ResNet-50 ("Build A")
Stable, efficient residual CNN baseline. Excellent for noisy/blurry underwater imagery and fast to train. Used weighted cross-entropy, label smoothing, and a OneCycleLR schedule. Served as the robust fallback when ConvNeXt convergence issues arose mid-competition. See `models/Resnet/`.

### ConvNeXt-Base
A "modernized" pure CNN borrowing ViT design ideas (large kernels, inverted bottlenecks). Promising in local validation but ran into convergence instability and hyperparameter sensitivity within the project timeline, so the team reverted to ResNet-50 for stability. See `models/ConvNeXT/`.

### YOLOv8 (Detection + Classification)
A two-stage pipeline: YOLOv8 first localizes organisms (ROI extraction), then a classification head (`YOLOv8m-cls` / `YOLOv8l-cls`) identifies the species. Includes a weighted ensemble of a 224px medium model and a 448px large model. Trained on a laptop RTX 4050 (6GB VRAM) with mixed-precision training to manage memory. See `models/YoloV8/`.

## ⚙️ Pipeline Summary

1. **Download & Crop** (`prep/download_images.py`) — Asynchronously fetches raw images via `httpx` and crops them to annotation bounding boxes, producing per-organism ROI images.
2. **Sort by Taxonomy** — Crops are organized into class-named subfolders based on `category_id`, making them compatible with `torchvision.datasets.ImageFolder`.
3. **Train** — Transfer learning from ImageNet-pretrained weights, with a custom linear head sized to the number of FathomNet classes, weighted loss, label smoothing, and a learning-rate schedule (OneCycleLR / CosineAnnealingLR).
4. **Inference** — Run the trained model in `eval()` mode over the test ROIs, map predicted indices back to category IDs, then to scientific concept names.
5. **Submit** — Export `annotation_id` → `concept_name` predictions to a Kaggle-format CSV.

## 🚀 Getting Started

### Requirements
```bash
pip install -r requirements.txt
```
Key dependencies: `torch`, `torchvision`, `torchaudio`, `ultralytics`, `pandas`, `numpy`, `opencv-python`, `httpx`, `coco-lib`, `tqdm`.

### Reproducing the Final Submission
The most direct path to reproduce the winning result is in `submission/`:

1. Create a `FathomNet` folder in Google Drive containing `dataset_train.json`, `dataset_test.json`, `train_rois.zip`, and `test_rois.zip`.
2. Open `submission/swinbmodel.py` in Google Colab (T4 GPU or better) — it will mount your Drive, extract and sort ROIs to local SSD, train the Swin-B model, and generate the submission CSV automatically.
3. To run locally instead: install dependencies, update the `DRIVE_BASE` path to a local dataset directory, remove the `drive.mount()` call, and run `python swinbmodel.py` (CUDA GPU with 12GB+ VRAM recommended for Swin-B).

Full setup details are in [`submission/read.md`](submission/read.md).

## 💡 Top Insights

* **Local Attention is Key:** Swin-B's window-based attention proved superior for resolving regional species details under shifting scales compared to standard CNNs or ViTs.
* **Data Pipeline Efficiency:** Moving from direct Drive streaming to local SSD storage was critical for accelerating GPU backpropagation iterations.
* **Stability vs. Novelty:** ConvNeXt showed theoretical promise but required more tuning time than was available; the team prioritized the more robust ResNet-50/Swin-B paths to protect leaderboard standing.
* **Hardware Constraints Shape Strategy:** The YOLOv8 track was tuned around a 6GB VRAM laptop GPU, demonstrating that batch size, resolution, and AMP all need to be co-tuned under real hardware limits.

## 📊 Further Reading

* [`results/model_comparison.md`](results/model_comparison.md) — Detailed architecture trade-off matrix (ResNet vs. ConvNeXt vs. Swin vs. YOLOv8).
* `models/<Architecture>/explanation.md` — Why each model was chosen.
* `models/<Architecture>/procedure.md` — Step-by-step training procedure per model.
* `models/Resnet/logs.md`, `models/ConvNeXT/logs.md` — Raw experimentation logs and decision rationale.

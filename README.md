# FathomNet 2025: Hierarchical Marine Species Classification
**Team Name:** Ikan Laut  
**Kaggle Ranking:** 11th Place Global[span_0](start_span)[span_0](end_span)  
**Best Public Score:** 2.53[span_1](start_span)[span_1](end_span)  
**Track:** 1 — Kaggle Competition (CVPR-FGVC 2025)[span_2](start_span)[span_2](end_span)
---
## 🌊 Project Overview
This repository contains the deep learning pipeline developed by team **Ikan Laut** for the FathomNet 2025 competition[span_3](start_span)[span_3](end_span). Our solution utilizes a pre-trained Swin Transformer-Base (Swin-B) architecture to perform fine-grained classification of deep-sea marine species[span_4](start_span)[span_4](end_span).
## 👥 The Team (Ikan Laut)

| Member | Primary Responsibility | Key Focus |
| :--- | :--- | :--- |
| **Nazhan** | Resnet User | ResNet-50 Optimization & ConvNeXt Experiments[span_5](start_span)[span_5](end_span) |
| **Akmal** | Detection Researcher | YOLOv8 Implementation & Localization[span_6](start_span)[span_6](end_span) |
| **Adibah** | Transformer Lead | Swin-B Architecture & Attention Mechanisms[span_7](start_span)[span_7](end_span) |

## 📈 Experimental Journey & Results
Our refinement process focused on shifting from standard CNN architectures to the Swin-B model, incorporating advanced techniques to handle class imbalance and noisy annotations[span_8](start_span)[span_8](end_span).

| Iteration | Architecture | Key Technique | Public Score | Status |
| :--- | :--- | :--- | :--- | :--- |
| 1 | ResNet-50 | Baseline | 3.45 | Baseline[span_9](start_span)[span_9](end_span) |
| 2 | ViT-B/16 | Standard | 2.92 | Experimental[span_10](start_span)[span_10](end_span) |
| 3 | Swin-B | Window-based Attention | 2.68 | Improved[span_11](start_span)[span_11](end_span) |
| 4 | **Swin-B** | **Weighted Loss + Smoothing** | **2.53** | **11th Place**[span_12](start_span)[span_12](end_span) |

## 📂 Directory Structure
* **`models/`**: Comprehensive folders for each architecture including:
    * `swinbmodel.py`: Core implementation of the Swin-B pipeline[span_13](start_span)[span_13](end_span).
    * `explanation.md`: Theoretical justification of the model[span_14](start_span)[span_14](end_span).
* **`results/`**: Leaderboard screenshots and performance visualizations[span_15](start_span)[span_15](end_span).
* **`archive/`**: Legacy code and historical submission attempts[span_16](start_span)[span_16](end_span).
## 🛠️ Environment & Setup
* **Platform:** Developed and trained on **Google Colab** (utilizing high-speed local SSD storage for I/O)[span_17](start_span)[span_17](end_span)[span_18](start_span)[span_18](end_span).
* **Data Source:** FathomNet 2025 Kaggle dataset (integrated via Google Drive)[span_19](start_span)[span_19](end_span)[span_20](start_span)[span_20](end_span).
* **Requirements:** Run `pip install -r requirements.txt` to replicate the environment[span_21](start_span)[span_21](end_span).
## 💡 Top Insights
* **Architecture Strategy:** Swin-B was selected for its ability to process localized marine organism details via shifted window self-attention, outperforming flat global attention models[span_22](start_span)[span_22](end_span).
* **Optimization Rigor:** We implemented `nn.CrossEntropyLoss` with dynamic inverse-frequency class weights and 0.1 label smoothing to combat class imbalance and overconfident predictions[span_23](start_span)[span_23](end_span).
* **Training Stability:** Using `AdamW` (weight decay 0.01) and `OneCycleLR` (max LR 4e-4) was crucial for stabilizing transformer weights during fine-tuning[span_24](start_span)[span_24](end_span).
---
*

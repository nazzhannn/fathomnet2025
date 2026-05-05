
---

# FathomNet 2025: Hierarchical Marine Species Classification
**Team Name:** Ikan Laut  
**Kaggle Ranking:** Top 30  
**Best Public Score:** 3.13 (Build A)  
**Track:** 1 — Kaggle Competition (CVPR-FGVC 2025)

---

## 🌊 Project Overview
This repository contains the deep learning pipeline developed by team **Ikan Laut** for the FathomNet 2025 competition. The objective is to automate the classification of ocean life using hierarchical labels. Our solution focuses on leveraging residual architectures and iterative hyperparameter tuning to navigate the complexities of underwater imagery.

## 👥 The Team (Ikan Laut)
| Member | Primary Responsibility | Key Focus |
| :--- | :--- | :--- |
| **Nazhan** | Lead Developer | ResNet-50 Optimization (Build A) & ConvNeXt Experiments |
| **Akmal** | Detection Researcher | YOLOv8 Implementation & Localization |
| **Adibah** | Transformer Lead | Swin-B Architecture & Attention Mechanisms |

## 📈 Experimental Journey & Results
Our progress was non-linear. We tested modern architectures (EfficientNet, ConvNeXt) but ultimately found that a highly-tuned ResNet-50 provided the best generalization for this dataset.

| Iteration | Architecture | Key Technique | Public Score | Status |
| :--- | :--- | :--- | :--- | :--- |
| 1 | ResNet-50 | Baseline (Epochs 1-5) | 7.59 | Baseline |
| 2 | EfficientNet-B0 | Experimental Pivot | Error | Discarded |
| 3 | ConvNeXt | Macro-Design implementation | N/A | Logged |
| 4 | **ResNet-50** | **Build A (Epoch 10 + AdamW)** | **3.13** | **Final Winner** |

## 📂 Directory Structure
* **`models/`**: Comprehensive folders for each architecture including:
    * `explanation.md`: Theoretical justification of the model.
    * `procedure.md`: Detailed training logs and hyperparameters.
* **`results/`**: Leaderboard screenshots and performance visualizations.
* **`archive/`**: Legacy code and historical submission attempts.
* **`REPORT_Assessment2_IkanLaut.pdf`**: The official submission report for MCTA4363.

## 🛠️ Environment & Setup
* **Platform:** Developed and trained strictly on **Google Colab**.
* **Data Source:** FathomNet 2025 Kaggle dataset (integrated via Google Drive).
* **Requirements:** Run `pip install -r requirements.txt` to replicate the environment.

## 💡 Top Insights
* **Stability > Novelty:** For this specific data distribution, the stability of ResNet-50 outperformed the more complex Transformer-based models.
* **Epoch Management:** We observed a significant "breakthrough" in score after reaching 10 epochs with specific weight decay settings.

---





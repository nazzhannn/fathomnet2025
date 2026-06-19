
# FathomNet 2025: Hierarchical Marine Species Classification
**Team Name:** Ikan Laut
**Kaggle Ranking:** 11th Place
**Best Public Score:** 2.53
**Track:** 1 — Kaggle Competition (CVPR-FGVC 2025)
## 🌊 Project Overview
This repository contains the deep learning pipeline developed by team **Ikan Laut** for the FathomNet 2025 competition. The objective is to automate the classification of ocean life using hierarchical labels. Our solution utilizes a pre-trained **Swin Transformer-Base (Swin-B)** architecture, optimized with dynamic class weighting and advanced regularization to navigate the complexities of underwater imagery.
## 👥 The Team (Ikan Laut)

| Member | Primary Responsibility | Key Focus |
| :--- | :--- | :--- |
| **Nazhan** | Resnet User | ResNet-50 Optimization & ConvNeXt Experiments |
| **Akmal** | Detection Researcher | YOLOv8 Implementation & Localization |
| **Adibah** | Transformer Lead | Swin-B Architecture & Attention Mechanisms | <br> ## 📈 Experimental Journey & Results <br> We progressed from standard CNN baselines to a high-performing Swin-B pipeline. Our final strategy incorporated local attention mechanisms and rigorous optimization techniques.
| Iteration | Architecture | Key Technique | Public Score | Status |
| :--- | :--- | :--- | :--- | :--- |
| 1 | ResNet-50 | Baseline | 3.45 | Baseline |
| 2 | ViT-B/16 | None | 2.92 | Experimental |
| 3 | Swin-B | Default (224x224) | 2.68 | Logged |
| 4 | **Swin-B** | **Dynamic Weights + Smoothing** | **2.53** | **Final** |

## 🛠️ Technical Strategy
 * **Swin-B Architecture:** We utilized shifted window self-attention to capture localized marine organism details, outperforming flat global attention models. We replaced the standard head with a custom linear layer to map latent features to specific biological categories.
 * **Preprocessing & I/O:** To bypass latency, we optimized data handling by extracting images directly to high-speed local Colab SSD storage and utilized on-the-fly metadata parsing for streamlined PyTorch loading.
 * **Optimization Rigor:**
   * **Imbalance Handling:** Implemented dynamic class weighting in nn.CrossEntropyLoss based on inverse directory frequencies.
   * **Regularization:** Applied 0.1 label smoothing to combat noisy annotations.
   * **Training Dynamics:** Employed AdamW (weight decay 0.01) with a OneCycleLR schedule, ramping the learning rate to 4e-4 to ensure stability.
## 📂 Directory Structure
 * **models/**: Comprehensive folders for each architecture including theoretical justifications and training logs.
 * **results/**: Leaderboard screenshots and performance visualizations.
 * **archive/**: Legacy code and historical submission attempts.
 * **prep/**: Scripts for downloading and preprocessing image data.
 * **REPORT_Assessment2_IkanLaut.pdf**: The official submission report for MCTA4363.
## 💡 Top Insights
 * **Local Attention is Key:** Swin-B’s window-based attention proved superior for resolving regional species details under shifting scales compared to standard CNNs or ViTs.
 * **Data Pipeline Efficiency:** Moving from direct Drive streaming to local SSD storage was critical for accelerating GPU backpropagation iterations.
*Generated based on project documentation.*

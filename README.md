# FathomNet 2025: Marine Species Classification
**Team Name:** Ikan Laut  
**Course:** MCTA4363 Deep Learning (Assessment 2)  
**Track:** 1 — Kaggle Competition  
**Current Ranking:** Top 30 (Public Score: 3.13)
---
## 👥 Team & Contributions
* **[Your Name]**: Lead Developer — ConvNeXt & ResNet implementations, Experiment Logging.
* **Akmal**: Detection Specialist — YOLOv8 architecture & localization.
* **Nabilah**: Transformer Researcher — Swin-B experimentation & performance tuning.
## 📈 Iterative Development Log
We followed an iterative approach to improve our public score from a baseline to a competitive ranking.

| Iteration | Model | Key Techniques | Public Score |
| :--- | :--- | :--- | :--- |
| 1 | **ResNet-50** | Baseline, ImageNet weights | 2.8x |
| 2 | **Swin-B** | Attention-based features | 3.01 |
| 3 | **YOLOv8** | Object detection / Localization | N/A (Internal) |
| 4 | **ConvNeXt** | **Stochastic Depth, AdamW, Heavy Augmentation** | **3.13** |

## 💡 Key Insights
1. **Model Choice:** While Transformers (Swin-B) are powerful, ConvNeXt provided better stability and higher scores on the benthic imagery features.
2. **Data Challenges:** Mounting Google Drive was essential for handling the large FathomNet dataset within the Colab environment.
3. **Augmentation:** Mixup and CutMix were critical in preventing overfitting given the specialized nature of underwater data.
## 📁 Repository Structure
* `experiments/`: Jupyter Notebooks for every model iteration.
* `src/`: Production-ready Python scripts for training and inference.
* `results/`: Leaderboard screenshots and evaluation metrics.
* `REPORT_Assessment2_IkanLaut.pdf`: The official documentation for Assessment 2.
## 🚀 How to Reproduce
1. Open any notebook in `experiments/` via Google Colab.
2. Mount your Google Drive containing the FathomNet data.
3. Install dependencies: `pip install -r requirements.txt`.
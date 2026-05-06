## Experimentation & Development Logs
### **Model Selection Rationale**
While larger architectures like ConvNeXt and EfficientNet were evaluated, **ResNet-50** was selected as the primary backbone for the final implementation.
 * **Stability:** Provided superior consistency given the hierarchical nature of FathomNet.
 * **Gradient Efficiency:** Skip-connections facilitated smoother gradient flow during the fine-tuning of specialized underwater features.
 * **Generalization:** Proved significantly less prone to overfitting on our specific data split compared to more complex, high-parameter models.
### **Training Iteration History**

| Phase | Description | Epochs | Results / Observations |
| :--- | :--- | :--- | :--- |
| **Phase 1** | **Baseline Setup** | 1 – 2 | Initial benchmarks yielded scores around **7.5**. Established stable pipeline connectivity. |
| **Phase 2** | **Incremental Tuning** | 7 – 10 | Observed a steady performance improvement. Scores dropped from **5.94** (7 epochs) to **5.52** (10 epochs). |
| **Phase 3** | **Final Optimization** | 15 | Identified **Build A** as the most robust configuration. Applied full augmentation and OneCycleLR. |

### **Final Performance Summary**
 * **Configuration:** Build A (Optimized ResNet-50)
 * **Peak Public Score:** **3.13**
 * **Conclusion:** The tuned ResNet-50 architecture in **Build A** successfully outperformed all experimental runs involving EfficientNet and ConvNeXt, achieving our best submission to date.

## Experimentation & Development Logs: ConvNeXt Pivot
### **Architecture Rationale**
We explored the **ConvNeXt** architecture specifically to leverage its **"Macro Design."** By combining the traditional efficiency of Convolutional Neural Networks (CNNs) with Transformer-inspired advancements—such as large kernels—we aimed to capture the intricate, fine-grained textures of deep-sea marine life more effectively than standard ResNet models.
### **Training & Iteration History**

| Phase | Description | Observed Outcome |
| :--- | :--- | :--- |
| **Architectural Pivot** | Attempted to integrate **ConvNeXt-Base** and **EfficientNet-B0** into the pipeline following initial ResNet-50 success. | Models showed promise in local validation but struggled with stability. |
| **Submission Trials** | Logged in history as "trying new." | Encountered **convergence issues** and technical errors within the Kaggle submission pipeline. |
| **Comparative Analysis** | Evaluation of resource-to-performance ratio. | Determined that ConvNeXt required significantly more **hyperparameter tuning** (specifically Learning Rate and Weight Decay) than the project timeline permitted. |

### **Strategic Conclusion**
 * **Final Decision:** Reverted to the **ResNet-50 "Build A"** configuration.
 * **Justification:** While ConvNeXt offers higher theoretical performance, the **robustness and reliability** of the optimized ResNet-50 provided the necessary stability to maintain our standing.
 * **Result:** By focusing on further refining "Build A," we successfully secured a **Top 30 ranking** in the competition.
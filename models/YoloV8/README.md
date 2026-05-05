## 🔍 Stage 1: YOLOv8 Localization & Pre-processing (Lead: Akmal)

As the detection researcher, my role was to establish the foundation of the pipeline. By isolating marine organisms from the deep-sea background, we transformed a noisy detection problem into a high-precision classification task.

### **Iterative Model Development Log**

| Experiment | Model Architecture | Resolution | Key Hyperparameters | Technique / Strategy | Public Score |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **01 (Baseline)** | YOLOv8m (Detection) | 640px | default | Established the 7.26 error baseline using single-stage detection. | 7.26 |
| **02 (Specialist)** | YOLOv8m-cls | 224px | `batch=32`, `lr=0.01` | **Two-stage Pipeline:** Implemented ROI extraction via `download.py` to focus on crops. | 3.77 |
| **03 (HD Detail)** | YOLOv8l-cls | 448px | `batch=8`, `imgsz=448` | **High-Res Focus:** Targeted fine-grained taxonomic features with increased model depth. | 3.82 |
| **04 (Ensemble)** | **Med + Large** | **Mixed** | **Weights: 0.7M / 0.3L** | **Weighted Averaging:** Combined the stability of 224px with the detail of 448px. | **3.60** |

---

## 🛠️ Technical Implementation & Hardware Optimization

A significant challenge was managing the training environment on a laptop **RTX 4050 with 6GB VRAM**. The following technical optimizations were critical:

*   **VRAM Management:** To handle high-resolution 448px training (Experiment 03), I systematically reduced the batch size from 32 to **8** to prevent "Out of Memory" (OOM) errors.
*   **Asynchronous ROI Extraction:** I authored the `download.py` script using `asyncio`. This automated the retrieval and cropping of thousands of Regions of Interest (ROIs) concurrently.
*   **Weighted Ensemble Logic:** I implemented a weighted probability averaging script to combine the outputs:
$$Final\ Prediction = (0.7 \times \text{Medium Model}) + (0.3 \times \text{Large HD Model})$$
*   **Automatic Mixed Precision (AMP):** Enabled `amp=True` during training to reduce memory consumption by approximately 30%.

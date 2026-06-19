
# README: FathomNet Build A+ Swin-B Classification
This repository contains the implementation for a Swin-Transformer (Swin-B) classification model designed for the FathomNet dataset. This "Build A+" configuration leverages advanced data augmentation, weighted cross-entropy loss to handle class imbalance, and the high-performance Swin-B architecture.
---
## 1. Google Drive Setup
To ensure the pipeline runs seamlessly, your Google Drive must be structured correctly. Create a folder named `FathomNet` in your root directory and upload the following files:

| File Name | Description |
| :--- | :--- |
| `dataset_train.json` | Training annotations metadata. |
| `dataset_test.json` | Test annotations metadata. |
| `train_rois.zip` | Archive containing training images. |
| `test_rois.zip` | Archive containing test images. |

Your folder structure should look like this:
```
/My Drive
  /FathomNet
    ├── dataset_train.json
    ├── dataset_test.json
    ├── train_rois.zip
    └── test_rois.zip
```

## 2. Google Colab Replication
 1. **Open Colab:** Upload swinbmodel.py (or copy the content into a new notebook).
 2. **GPU Runtime:** Ensure your Colab runtime is set to **T4 GPU** or higher.
 3. **Authentication:** The script will automatically prompt you to mount your Google Drive upon execution.
 4. **Run Cells:** Execute the cells in order to perform:
   * Mounting your drive.
   * Extracting ZIP files to local high-speed SSD storage.
   * Sorting images into taxonomic folders.
   * Training and generating the final submission file.
## 3. Running Locally
If you prefer to run this project on a local machine, follow these steps:
### Prerequisites
 * **Python 3.10+** installed.
 * **CUDA-enabled GPU** (Recommended: 12GB+ VRAM for Swin-B).
 * **Libraries:** Install via terminal: pip install torch torchvision pandas tqdm pillow.
### Configuration Changes
 1. **Paths:** Update DRIVE_BASE in the "PHASE 1" section to point to your local dataset directory.
 2. **Google Drive Mounting:** Comment out or remove the drive.mount('/content/drive') block.
 3. **Execution:** Run the script using python swinbmodel.py.
### Local Tips
 * **Performance:** Ensure you have sufficient RAM or SSD storage to avoid bottlenecks during training.
 * **Environment:** Use a virtual environment (venv or conda) to manage dependencies.

```
```

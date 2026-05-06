# Implementation Procedure
## Phase 1: Environment Setup
 * **Drive Integration:** Mount Google Drive to establish a persistent link to dataset ZIP files and JSON metadata.
 * **Dependencies:** Import the PyTorch ecosystem (torch, torchvision) for deep learning and pandas for metadata manipulation.
 * **Hardware Acceleration:** Initialize the DEVICE variable to cuda to leverage NVIDIA GPU acceleration, which is essential for deep residual networks.
## Phase 2: Data Preparation
 * **I/O Optimization:** Unzip training and testing ROIs (Regions of Interest) directly into the local environment storage to bypass cloud latency.
 * **Taxonomic Organization:**
   1. Parse the dataset_train.json file.
   2. Scan the training imagery directory.
   3. Programmatically sort images into a hierarchical sub-folder structure based on category_id, making them compatible with PyTorch’s ImageFolder class.
## Phase 3: Model Architecture & Training
 * **Transfer Learning:** Load a **ResNet-50** backbone pre-trained on ImageNet to utilize existing feature extraction capabilities.
 * **Custom Classification Head:** Replace the final Fully Connected (FC) layer with a new linear layer tailored to the exact number of marine classes in the FathomNet dataset.
 * **Optimization Suite:**
   * **Optimizer:** Use **AdamW** for superior weight decay and convergence.
   * **Loss Function:** Implement **Weighted Cross-Entropy** to mitigate the "long-tail" effect of rare species.
 * **The Training Loop:** Execute for 15 epochs, incorporating:
   * **Data Augmentation:** Real-time random flips and color jitters to improve model robustness.
   * **OneCycleLR:** Update the learning rate per batch to optimize the gradient descent path.
## Phase 4: Inference & Submission
 * **Validation Loading:** Re-initialize the model using the saved .pth weights from the best-performing epoch.
 * **Inference Constraints:** Set the model to .eval() mode, freezing batch normalization and dropout layers for consistent predictions.
 * **Prediction Pipeline:**
   1. Resize test images to 224 \times 224 pixels.
   2. Perform a forward pass to generate class logits.
   3. Map the resulting index to the biological **Concept Name**.
 * **Export:** Generate a final CSV submission file containing the annotation_id and its corresponding taxonomic prediction.

# Implementation Procedure: ConvNeXt Pipeline
## Phase 1: Environment Setup
 * **Hardware Acceleration:** Configure the Google Colab runtime to utilize a high-performance **GPU (T4, L4, or A100)**. This is necessary to handle the computational intensity of the ConvNeXt-Base architecture.
 * **Storage Mounting:** Establish a secure link to Google Drive to retrieve the dataset files stored within the /FathomNet directory.
 * **Workspace Initialization:** Create temporary local directories (e.g., /content/train_data_sorted) to manage the data flow and ensure fast I/O during the training session.
## Phase 2: Data Pre-processing
 * **Archive Extraction:** Unzip the train_rois.zip and test_rois.zip files into the local disk to maximize data throughput.
 * **Taxonomic Relocation:** Programmatically sort images into class-specific subfolders. This structure allows the datasets.ImageFolder class to automatically map folder names to categorical labels.
 * **Input Standardization:**
   * **Resizing:** Transform images to 224 \times 224 pixels.
   * **Normalization:** Apply ImageNet-specific mean and standard deviation values to align the data distribution with the pre-trained model's expectations.
## Phase 3: Model Training
 * **Initialization:** Load the **ConvNeXt-Base** backbone and reconfigure the output head to match the specific number of classes in the target dataset.
 * **Imbalance Correction:** Calculate specific class frequencies to generate inverse-frequency weights for the loss function, ensuring equitable learning across rare and common species.
 * **The Training Loop:**
   1. **Forward Pass:** Input data through the network to generate predictions.
   2. **Weighted Loss:** Calculate error using the pre-computed weights.
   3. **Backpropagation:** Update the network weights based on the gradient of the loss.
   4. **Scheduler Step:** Apply **CosineAnnealingLR** to smoothly decay the learning rate toward the end of the training cycle.
 * **Checkpointing:** Periodically save the trained .pth state-dict to Google Drive to prevent progress loss from session timeouts.
## Phase 4: Prediction & Submission
 * **Evaluation Mode:** Toggle the model to .eval(). This critical step disables dropout and freezes batch normalization layers for deterministic inference.
 * **Batch Inference:** Process the test dataset using the training transformations (excluding random augmentations) to maintain consistency.
 * **Taxonomic Mapping:** Convert the numerical output indices into human-readable concept_name strings.
 * **Submission Export:** Consolidate the annotation_id and predicted names into a final CSV file formatted for competition submission.

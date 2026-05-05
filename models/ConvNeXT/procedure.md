procedure.md
Phase 1: Environment Setup
Hardware Acceleration: Ensure the Google Colab runtime is set to GPU (T4, L4, or A100).

Storage Mounting: The script mounts Google Drive to access the dataset files stored in the /FathomNet directory.

Local Directory Creation: Temporary folders (/content/train_data_sorted, etc.) are created to handle the data flow during the session.

Phase 2: Data Pre-processing
Extraction: Unzip train_rois.zip and test_rois.zip.

Relocation: Images are moved into class-specific subfolders based on the JSON metadata. This is required so that datasets.ImageFolder can automatically assign labels.

Normalization: Images are resized to 224x224 and normalized using ImageNet mean and standard deviation values to align with what the pre-trained ConvNeXt model expects.

Phase 3: Model Training
Initialization: Load the convnext_base model and modify the output head.

Imbalance Correction: Calculate class counts to generate loss weights.

Training Loop:

Perform forward passes to get predictions.

Calculate loss using the weighted criterion.

Perform backpropagation to update model weights.

Step the CosineAnnealingLR scheduler to reduce the learning rate over time.

Checkpointing: Save the trained .pth file to Google Drive to avoid losing progress.

Phase 4: Prediction & Submission
Evaluation Mode: Switch the model to eval() to disable dropout and batch normalization updates.

Batch Inference: Iterate through the test images, applying the same transformations used during training (without the random augmentations).

Mapping: Convert the prediction indices to the final concept_name strings.

Export: Save the results into a CSV file formatted for competition submission
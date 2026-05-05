procedure.md
Phase 1: Environment Setup
Drive Integration: Mount Google Drive to access the dataset ZIP files and JSON metadata.

Dependencies: Import standard PyTorch libraries for computer vision (torchvision) and data manipulation (pandas).

Hardware Check: Assign the DEVICE variable to cuda to ensure the training happens on the NVIDIA GPU.

Phase 2: Data Preparation
Extraction: Unzip the training and testing ROIs into the local Colab disk.

Taxonomic Sorting:

Read dataset_train.json.

Iterate through every image in the training folder.

Move images into sub-folders named after their category_id.

Phase 3: Model Architecture & Training
Model Loading: Load a ResNet-50 model pre-trained on ImageNet.

Head Replacement: Modify the final "Fully Connected" (FC) layer to output the specific number of marine classes found in the FathomNet dataset.

Optimization Strategy:

Initialize the AdamW optimizer (a version of Adam with better weight decay).

Define the Weighted Cross-Entropy loss to handle class imbalance.

Training Execution: Run for 15 epochs. In each epoch:

Apply random augmentations (flips, color jitters).

Perform forward pass and calculate loss.

Perform backpropagation to update weights.

Update the OneCycleLR scheduler.

Phase 4: Prediction & Export
Model Loading: Re-load the saved .pth weights to ensure we use the best version of the model.

Evaluation Mode: Set model.eval() to freeze batch normalization and dropout layers.

Image Processing: Loop through the test folder, resize each image to 224x224, and run it through the model.

CSV Generation:

Retrieve the predicted class index.

Map the index to the taxonomic "Concept Name."

Save the annotation_id and name into a CSV file for submission.
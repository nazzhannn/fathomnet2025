explanation.md
Core Concept

This script implements a deep learning pipeline using the ConvNeXt-Base architecture to classify marine organisms from the FathomNet dataset. ConvNeXt is a modern "pure convolutional" neural network that adopts many design choices from Vision Transformers (ViT) to achieve state-of-the-art performance while maintaining the efficiency of standard Convolutions.

Key Components
1. Data Pipeline & Organization

Dynamic Extraction: The script extracts image data from ZIP files to the local Colab environment to speed up training (reading from local NVMe is significantly faster than reading from Google Drive over a network).

Metadata Mapping: It parses dataset_train.json to link specific annotation IDs to their corresponding category IDs, effectively sorting the flat image folder into a directory structure compatible with PyTorch's ImageFolder.

2. Model Architecture: ConvNeXt-Base

Pre-trained Weights: It uses IMAGENET1K_V1 weights as a starting point (Transfer Learning), which allows the model to leverage features like edges, textures, and shapes learned from 1.2 million general images.

Custom Head: The final classification layer is replaced with a nn.Linear layer matching the number of specific classes in the marine dataset.

3. Advanced Training Techniques

Augmentation: Uses RandomHorizontalFlip, RandomRotation, and ColorJitter to artificially increase dataset variety and prevent overfitting.

Weighted Cross-Entropy: Since marine datasets often have many common species and few rare ones, class weights are calculated to ensure the model doesn't ignore underrepresented categories.

Label Smoothing: Prevents the model from becoming "overconfident" in its predictions, which improves generalization to the test set.

AdamW & Cosine Annealing: Uses a decoupled weight decay optimizer (AdamW) and a learning rate scheduler that follows a cosine curve, helping the model converge to a better global minimum.

4. Inference Logic

The model processes the test images in evaluation mode (model.eval()).

It maps the numerical index predicted by the model back to the actual "Concept Name" (e.g., specific species name) using the metadata provided in the JSON file
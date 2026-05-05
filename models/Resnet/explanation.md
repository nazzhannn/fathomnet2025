explanation.md
Core Concept
This script implements a complete machine learning pipeline using ResNet-50 (Residual Network with 50 layers) to classify deep-sea imagery from the FathomNet dataset. The goal is to identify marine organisms by training on "Regions of Interest" (ROIs)—small cropped images of specific animals.

Key Components
1. Residual Learning (ResNet-50)
ResNet-50 is a powerful convolutional neural network that uses "skip connections" (or identity shortcuts). These allow the model to learn residuals, which prevents the "vanishing gradient" problem and allows for much deeper networks compared to traditional architectures.

2. Strategic Data Handling

Local SSD Processing: The code moves data from Google Drive to the local /content/ directory. This is critical because Google Drive's I/O speeds are slow; training directly from Drive can make the GPU wait for data, tripling training time.

Folder-Based Sorting: PyTorch's ImageFolder class expects a directory structure where each folder name is a class label. The script programmatically maps the flat JSON metadata to a nested folder structure.

3. Advanced Training Features

Imbalance Handling: Deep-sea datasets often have "long-tail" distributions (a few common species and many rare ones). The script uses Weighted Cross-Entropy, giving higher importance to rare classes so the model doesn't just guess the most common species every time.

OneCycle Learning Rate Policy: Instead of a static learning rate, the OneCycleLR scheduler starts low, ramps up to find the best gradients, and then tapers off to fine-tune the weights.

Label Smoothing: By setting label_smoothing=0.1, we tell the model not to be 100% sure of its labels. This prevents overfitting and helps the model generalize better to noisy or blurry underwater images.

4. Inference & Mapping
The final stage converts the model's numerical output back into human-readable scientific names (concept_name). It links the internal class index to the category_id and finally to the metadata name provided in the original JSON
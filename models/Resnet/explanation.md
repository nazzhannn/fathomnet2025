# ResNet-50 Model Explanation
## What is ResNet-50?
 * **ResNet-50 (Residual Network)** is a deep convolutional neural network that is 50 layers deep.
 * It introduces **Residual Learning** through "skip connections" (or identity shortcuts) that allow the gradient to flow through the network without disappearing.
 * By learning *residuals* (the difference between the input and output of a layer) rather than the direct mapping, the model avoids the **vanishing gradient problem**, allowing it to be much deeper and more accurate than traditional architectures.
## Why Suitable for FathomNet?
 * **Efficiency:** FathomNet datasets can be massive; ResNet-50 offers a high-performance balance between computational speed and classification accuracy.
 * **Deep-Sea Robustness:** The model is excellent at extracting features from noisy or blurry underwater images where fine details of marine organisms might be obscured by haze.
 * **Transfer Learning Gold Standard:** As one of the most widely used backbones pretrained on ImageNet, it provides a very stable starting point for fine-tuning on specialized biological datasets.
## Our Implementation
 * **Weighted Cross-Entropy:** Implemented to handle the "long-tail" distribution of marine species, ensuring rare organisms are not ignored by the model.
 * **Label Smoothing:** Applied at a factor of 0.1 to prevent the model from becoming overconfident, which improves generalization on varied deep-sea imagery.
 * **OneCycle Learning Rate:** Used a dynamic scheduler to find the most efficient path to convergence, starting with a warm-up and ending with fine-tuning.
 * **Local SSD Migration:** Optimized the pipeline by moving data from Google Drive to local storage to eliminate I/O bottlenecks and maximize GPU utilization.
**Strengths:** Highly stable training, excellent feature extraction for ROIs, and very efficient inference speed.
**Challenges:** Can struggle with extremely small organisms if the resolution is too low; requires careful class-weighting due to the massive species imbalance in FathomNet.

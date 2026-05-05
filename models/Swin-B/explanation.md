# Swin-B Model Explanation

## What is Swin Transformer?
- Swin-B (Shifted Window Transformer) is a powerful Vision Transformer.
- It uses **hierarchical** feature extraction (like a pyramid) — good for seeing both small details and big picture.
- It divides the image into small windows and calculates attention inside each window, then shifts the windows to connect information across the whole image.
- "Shifted Windows" allow efficient attention across the image without huge computation cost.

## Why Suitable for FathomNet?
- Underwater images have haze, varying light, and complex backgrounds.
- Hierarchical design helps classify marine species at different taxonomy levels (the competition uses hierarchical scoring).
- Strong at fine-grained classification (telling apart similar-looking sea creatures).
- Strong backbone pretrained on ImageNet, easy to fine-tune.

## Our Implementation
- Used Swin-B backbone from HuggingFace/Timm.
- Added custom classification head for 79 hierarchical categories.
- Trained with transfer learning (pretrained on ImageNet).
- Applied data augmentation for underwater variations (flip, rotate, brightness, contrast).

**Strengths**: Excellent feature extraction, good for domain shift (shallow → deep sea).\
**Challenges**: Higher GPU memory usage, sometimes slower training, can overfit.

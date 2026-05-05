# Swin-B Training Procedure & Results

## Training Setup
- Model: microsoft/swin-base-patch4-window7-224
- Image size: 224x224
- Optimizer: AdamW (lr = 1e-4)
- Scheduler: ReduceLROnPlateau
- Epochs: 8–12
- Batch size: 16–32 (GPU memory limit)
- Loss: CrossEntropyLoss (with hierarchical weighting planned)
- Augmentations: RandomFlip, RandomRotation, ColorJitter -brightness/contrast (important for underwater variation)

## Experiments Summary
- Baseline (basic training): ~6.8 Hierarchical Distance
- + Strong augmentations: improved to ~5.2
- + LR scheduler + more epochs: reached ~4.8 (further drop)
- Longer training (12 epochs): slight overfitting observed
- Compared to ResNet-50 (team best ~3.13): Swin-B performed decently but needed more regularization (dropout, weight decay)

## Key Insights
- Swin-B's attention mechanism allows it to learn rich features (occluded or low-light creatures).
- Performs well on clear images but struggles more with very dark/hazy underwater photos.
- Uses more memory than CNNs (ResNet/ConvNeXt).
- Training was slower and used more GPU memory.
- Good candidate for future ensemble with ResNet.

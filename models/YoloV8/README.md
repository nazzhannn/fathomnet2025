Experiment,Model Architecture,Resolution,Key Hyperparameters,Technique / Strategy,Public Score
01 (Baseline),YOLOv8m (Detection),640px,default,Established the 7.26 error baseline using single-stage detection.,7.26
02 (Specialist),YOLOv8m-cls,224px,"batch=32, lr=0.01",Two-stage Pipeline: Implemented ROI extraction via download.py to focus on crops.,3.77
03 (HD Detail),YOLOv8l-cls,448px,"batch=8, imgsz=448",High-Res Focus: Targeted fine-grained taxonomic features with increased model depth.,3.82
04 (Ensemble),Med + Large,Mixed,Weights: 0.7M / 0.3L,Weighted Averaging: Combined the stability of 224px with the detail of 448px.,3.60

Project Overview
This project implements a multi-granularity rock image classification system using the ConvNeXtV2 Large pre-trained model. The system simultaneously predicts:

3 main rock categories (coarse-grained classification)
20,000 fine-grained subcategories
The method demonstrates practical value for geological analysis and resource evaluation, particularly in distinguishing visually similar but mineralogically distinct rock types.

Key Features
​​Dual-task learning framework​​: Shared backbone with parallel classification heads
​​Advanced training strategies​​:
Mixed precision training (AMP)
Exponential moving average (EMA)
RandAugment data augmentation
Label smoothing (α=0.1)
​​Optimized loss function​​: Weighted combination (λ=0.4) of main and subcategory losses
​​Efficient optimization​​: AdamW with cosine annealing learning rate schedule
Model Architecture
Trunk Network
​​Base Model​​: ConvNeXtV2 Large (from timm library)
​​Pre-trained Weights​​: fcmae_ft_in22k_in1k_384
​​Parameter Count​​: 227,164,451
Classification Heads
​​Main Class Head​​:
3 output classes
CrossEntropyLoss
​​Sub-class Head​​:
20,000 output classes
Label Smoothing (0.1)


Training Configuration
Data Augmentation
​​Training Stage​​:

RandomResizedCrop (224×224)
RandomHorizontalFlip
RandAugment (num_ops=2, magnitude=9)
​​Testing Stage​​:

Resize (256×256) + CenterCrop (224×224)
Optimization
​​Optimizer​​: AdamW (lr=1e-4, weight_decay=1e-4)
​​Learning Rate Schedule​​: Cosine annealing with 2-epoch warmup
​​Batch Size​​: 30
​​Epochs​​: 30 (with early stopping)


Performance
​​Best Main Class Accuracy​​: 76.93%
​​Training Stability​​: Achieved through EMA and mixed precision training


Dataset
​​Source​​: /shareddata/project/dataset
​​Classes​​:
3 main categories
~20,000 subcategories
​​Normalization​​:
normalized_pixel = (pixel - μ)/σ
where μ=[0.485,0.456,0.406], σ=[0.229,0.224,0.225]
Hardware Requirements
​​GPU​​: NVIDIA GPU with ≥40GB VRAM recommended
​​Reproducibility​​: Fixed random seed (114514)
Cloud Storage
Project notebook available at:

​​Link​​: https://pan.baidu.com/s/1ujqFRPWLV8kNkmtt1x_X3g
​​Extraction Code​​: q4tq
Future Work
Exploration of self-supervised pretraining to reduce labeled data dependency
Extension to additional geological image analysis tasks

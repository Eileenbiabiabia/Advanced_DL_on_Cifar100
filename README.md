# Project Report

This project explores various strategies to improve image classification accuracy and efficiency, including data augmentation, model compression, fast training techniques, knowledge distillation, and network structure optimization. Below is a concise summary.

## Data Augmentation

1. **Cutout**:  
   - Idea: Randomly mask out patches in images, forcing the network to rely on more diverse features.  
   - Result: Slight accuracy improvement, retained in the final model.

2. **Mixup**:  
   - Idea: Linearly combine pairs of samples and labels to encourage linear behavior between training examples.  
   - Result: Slight accuracy improvement, retained in the final model.

3. **ColorJitter (Brightness/Contrast/Saturation/Hue)**:  
   - Idea: Randomly adjust image brightness, contrast, saturation, and hue.  
   - Result: Accuracy around 68% without clear improvement. Potentially introduced non-informative data, reducing final test performance.

4. **Flip Transformations**:  
   - Various flipping operations applied to training and testing transforms did not improve accuracy and were discarded.

## Model Compression & Fast Training

1. **Quantization**:  
   - Idea: Convert weights from float32 to int8 to reduce model size and accelerate inference.  
   - Result: Model size reduced to 1/4, but accuracy significantly dropped. Further optimization of quantization strategy is needed.

2. **Fast Training Strategies (Ghost Normalization, CELU)**:  
   - Replaced ReLU with CELU, improving convergence speed without losing accuracy.  
   - Introduced Ghost Normalization to mitigate generalization gap issues associated with large batch sizes.  
   - Added Dropout to reduce overfitting.  
   - Final outcome: Maintained accuracy (~75.9%) while reducing training time by ~40%.

## Knowledge Distillation

- Idea: Use a high-accuracy teacher model’s soft targets to guide a lighter student model.  
- Current result: Distillation did not improve student accuracy, potentially due to unsuitable distillation temperature or other hyperparameter settings. Further tuning is required.

## Network Structure

1. **ParNet, SqueezeNet, Inception**:  
   - Explored parallel subnetworks (Inception-style) and SqueezeNet’s channel compression.  
   - For small images (CIFAR100), adapted the network depth and complexity.
   - Adopted InceptionA and InceptionB modules with 1x1 convolutions for channel compression, replaced average pooling with max pooling, and experimented with smoother activation functions like SiLU/CELU.

2. **Final Model Improvements**:  
   - Based on Inception modules, integrated SqueezeNet’s channel compression via 1x1 convolutions.  
   - Replaced average pooling with max pooling for better feature extraction.  
   - Used smooth activation functions (SiLU/CELU) for better training efficiency.  
   - Adjusted learning rates and training epochs (in total 120 epochs) for optimal convergence and accuracy.

---

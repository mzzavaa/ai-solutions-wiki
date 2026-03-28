---
title: "Convolutional Neural Network"
description: "How CNNs extract spatial features from images and why architectures like ResNet, EfficientNet, and MobileNet remain foundational in computer vision."
date: 2026-03-28
categories: [Glossary]
tags: [CNN, computer-vision, deep-learning, image-recognition, ResNet]
related:
  - glossary/deep-learning
  - glossary/neural-network
  - glossary/vision-transformer
  - glossary/computer-vision
---

A convolutional neural network (CNN) is a deep learning architecture designed to process grid-structured data, most commonly images. CNNs use learnable filters (kernels) that slide across the input to detect spatial patterns such as edges, textures, and shapes. This weight-sharing mechanism dramatically reduces parameter counts compared to fully connected networks, making CNNs practical for high-resolution inputs.

## How It Works

A CNN typically alternates between convolutional layers, which apply filters to produce feature maps, and pooling layers, which downsample spatial dimensions. Early layers capture low-level features (edges, corners), while deeper layers compose these into high-level concepts (faces, objects). A classification head at the end maps features to output categories.

**ResNet** (2015) introduced skip connections that enable training networks with hundreds of layers by mitigating vanishing gradients. **VGG** demonstrated that stacking small 3x3 filters outperforms larger kernels. **Inception** (GoogLeNet) uses parallel filter sizes within each layer to capture features at multiple scales. **EfficientNet** systematically scales depth, width, and resolution together for optimal accuracy-per-FLOP. **MobileNet** uses depthwise separable convolutions to achieve competitive accuracy at a fraction of the compute, making it suitable for edge devices and mobile phones.

## Why It Matters

CNNs transformed computer vision from hand-engineered feature pipelines to end-to-end learned systems. They power image classification, object detection, medical imaging, autonomous driving, and quality inspection in manufacturing. While vision transformers have matched or exceeded CNN accuracy on large datasets, CNNs remain preferred when training data is limited or inference must run on resource-constrained hardware.

## Practical Considerations

For production deployments, architecture choice depends on the compute budget. MobileNet and EfficientNet-Lite target mobile and edge inference. ResNet remains a reliable baseline for server-side workloads. Pre-trained CNN backbones from ImageNet are widely available and transfer well to domain-specific tasks, reducing both training time and data requirements. Many production vision systems still use CNN feature extractors even within larger multimodal pipelines.

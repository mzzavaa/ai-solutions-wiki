---
title: "Activation Function"
description: "What activation functions are, how they enable neural networks to learn non-linear patterns, and which functions are used in modern architectures."
date: 2026-03-28
categories: [Glossary]
tags: [activation-function, neural-network, deep-learning, ReLU, training]
related:
  - glossary/neural-network
  - glossary/deep-learning
  - glossary/gradient-descent
---

An activation function is a mathematical function applied to the output of each neuron in a neural network. It introduces non-linearity, which enables the network to learn complex patterns. Without activation functions, a multi-layer neural network would be equivalent to a single linear transformation, regardless of depth.

## Common Activation Functions

**ReLU (Rectified Linear Unit)** outputs the input directly if positive, or zero if negative: f(x) = max(0, x). ReLU is the default choice for hidden layers in most architectures due to its computational simplicity and effective gradient properties. Its main weakness is "dying neurons" - neurons that output zero for all inputs and stop learning.

**GELU (Gaussian Error Linear Unit)** is a smooth approximation of ReLU that is the standard activation in transformer models (GPT, BERT, Claude). It weights inputs by their probability under a Gaussian distribution, providing a smoother gradient landscape that benefits large model training.

**Sigmoid** squashes output to the range (0, 1). Used for binary classification output layers and gating mechanisms (e.g., in LSTMs). Rarely used in hidden layers due to vanishing gradient problems at extreme values.

**Softmax** converts a vector of raw scores into a probability distribution that sums to one. Used as the output activation for multi-class classification and for attention weight computation in transformers.

**Tanh** squashes output to (-1, 1). Historically used in RNNs, now largely supplanted by ReLU and GELU in modern architectures.

## Why It Matters

Activation function choice affects training stability, convergence speed, and model performance. For technical leaders, this is typically a detail handled by model architects, but understanding it helps when interpreting model configurations or troubleshooting training issues.

## Practical Guidance

For most new architectures, use GELU for transformers and ReLU (or its variants like Leaky ReLU, SiLU/Swish) for convolutional networks. Use sigmoid for binary output layers and softmax for multi-class output layers. If training is unstable or neurons are dying, switching the activation function is one diagnostic step worth trying.

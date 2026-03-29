---
title: "Gradient Descent"
description: "What gradient descent is, how it optimizes neural networks, and the variants used in modern deep learning."
date: 2026-03-28
categories: [Glossary]
tags: [gradient-descent, optimization, deep-learning, training, backpropagation]
related:
  - glossary/backpropagation
  - glossary/loss-function
  - glossary/neural-network
  - glossary/hyperparameter-tuning
---

Gradient descent is the optimization algorithm used to train neural networks. It iteratively adjusts model parameters (weights) in the direction that reduces the loss function, moving toward a set of weights that produces accurate predictions. Virtually all neural network training uses some variant of gradient descent.

## How It Works

The loss function measures how wrong the model's predictions are. The gradient of the loss with respect to each weight indicates how much and in which direction that weight should change to reduce the loss. Gradient descent computes these gradients (via backpropagation) and updates each weight by subtracting a fraction of its gradient. The fraction is the learning rate - a critical hyperparameter.

**Batch gradient descent** computes the gradient over the entire training set before each update. Precise but slow and memory-intensive.

**Stochastic gradient descent (SGD)** computes the gradient from a single example. Fast but noisy - updates have high variance.

**Mini-batch gradient descent** computes the gradient over a small batch (32-512 examples). The standard practice: balances noise and efficiency, and maps well to GPU parallelism.

## Modern Optimizers

Plain SGD is rarely used alone. Modern optimizers add momentum and adaptive learning rates:

**Adam** (Adaptive Moment Estimation) maintains per-parameter learning rates based on first and second moment estimates of the gradient. It is the default optimizer for most deep learning tasks due to its robustness across hyperparameter choices.

**AdamW** adds decoupled weight decay to Adam, improving generalization. Widely used for transformer training.

**SGD with momentum** accumulates a running average of past gradients, smoothing updates and accelerating convergence. Sometimes preferred for computer vision tasks where it achieves slightly better generalization than Adam.

## Why It Matters

For technical leaders, gradient descent determines training cost and model quality. The learning rate is the single most important hyperparameter: too high and training diverges, too low and training takes excessively long or gets stuck. Learning rate schedules (warmup, cosine decay) are standard practice for achieving good results. Understanding these fundamentals helps you interpret training curves, diagnose training failures, and make informed decisions about training infrastructure requirements.

---
title: "Neural Network"
description: "What neural networks are, how they learn from data, and where they fit in modern AI system architecture."
date: 2026-03-28
categories: [Glossary]
tags: [neural-network, deep-learning, machine-learning, AI]
related:
  - glossary/deep-learning
  - glossary/activation-function
  - glossary/backpropagation
  - glossary/loss-function
---

A neural network is a computational model inspired by biological neurons, consisting of layers of interconnected nodes (neurons) that learn to map inputs to outputs by adjusting connection weights during training. Neural networks are the foundation of modern AI, powering everything from image recognition to language models.

## How It Works

A neural network has three types of layers: an input layer (receives raw data), one or more hidden layers (perform computations), and an output layer (produces predictions). Each neuron receives inputs, multiplies them by learned weights, adds a bias term, and passes the result through an activation function that introduces non-linearity.

During training, the network processes examples, compares its predictions to correct answers using a loss function, and adjusts weights via backpropagation to reduce the error. This process repeats over many iterations (epochs) until the network achieves acceptable accuracy on held-out validation data.

## Types of Neural Networks

**Feedforward networks** pass information in one direction, input to output. They are the simplest form and work for tabular data and basic classification.

**Convolutional neural networks (CNNs)** use spatial filters to detect patterns in images and are the standard for computer vision tasks.

**Recurrent neural networks (RNNs)** process sequential data by maintaining internal state, though they have been largely supplanted by transformers for most sequence tasks.

**Transformers** use attention mechanisms to process sequences in parallel and are the architecture behind modern language models.

## Why It Matters

For technical leaders, neural networks are the building block of nearly every AI capability your organization will deploy. You rarely build neural networks from scratch - instead, you use pre-trained foundation models or fine-tune existing architectures. Understanding the fundamentals helps you evaluate tradeoffs: model size versus inference cost, training data requirements, and the distinction between what neural networks learn well (pattern recognition, generation) and what they struggle with (precise arithmetic, guaranteed factual accuracy).

## When to Use Neural Networks

Neural networks excel when you have large amounts of data, the relationships between inputs and outputs are complex and non-linear, and you can tolerate probabilistic rather than deterministic outputs. For small datasets or problems requiring interpretable decisions, simpler models (logistic regression, decision trees) may be more appropriate.

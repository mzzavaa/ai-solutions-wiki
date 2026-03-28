---
title: "Recurrent Neural Network"
description: "How RNNs, LSTMs, and GRUs process sequential data, the vanishing gradient problem, and where recurrent models still apply."
date: 2026-03-28
categories: [Glossary]
tags: [RNN, LSTM, GRU, sequence-modeling, deep-learning]
related:
  - glossary/transformer-architecture
  - glossary/state-space-model
  - glossary/temporal-convolutional-network
  - glossary/neural-network
---

A recurrent neural network (RNN) is a neural architecture that processes sequential data by maintaining a hidden state that carries information from previous time steps. At each step, the network takes the current input and the prior hidden state to produce an output and an updated state. This makes RNNs naturally suited to time series, speech, and language tasks where order matters.

## How It Works

The basic RNN applies the same weight matrices at every time step, creating a chain of computations across the sequence. However, standard RNNs struggle with long sequences because gradients either vanish (shrink to near zero) or explode (grow uncontrollably) during backpropagation through time.

**Long Short-Term Memory (LSTM)** networks address this with a gating mechanism: input, forget, and output gates control what information to store, discard, or pass forward in a dedicated cell state. This allows LSTMs to maintain relevant context over hundreds of time steps. **Gated Recurrent Units (GRUs)** simplify the LSTM by merging the cell state and hidden state, using only reset and update gates, which reduces parameters while achieving comparable performance on many tasks.

## Why It Matters

RNNs were the dominant architecture for sequence modeling before transformers. They powered early machine translation (seq2seq models), speech recognition, and text generation. Understanding RNNs remains important because many production systems in time-series forecasting, sensor data processing, and embedded applications still use LSTM or GRU variants, particularly where low latency and small model size are required.

## Practical Considerations

RNNs process tokens sequentially, which limits training parallelism and makes them slower to train than transformers on large datasets. For new projects, transformers or state-space models are typically preferred for long sequences. However, RNNs remain competitive for short sequences on edge devices where model size is constrained. If maintaining a legacy RNN system, consider benchmarking against a small transformer or temporal convolutional network to evaluate whether migration offers meaningful improvements.

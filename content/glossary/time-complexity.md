---
title: "Time Complexity (Big-O Notation)"
description: "How to reason about algorithm efficiency using Big-O notation, and why it matters when processing thousands of video frames or building RAG retrieval systems."
date: 2026-03-26
categories: [Glossary]
tags: [glossary, algorithms, fundamentals, performance]
related:
  - guides/sorting-algorithms-for-ai
  - glossary/data-structures
  - patterns/tiered-analysis
---

Big-O notation describes how an algorithm's runtime grows as input size increases. It is the standard vocabulary for discussing algorithm efficiency and a necessary tool for any developer working on systems that process non-trivial amounts of data.

## The Common Complexity Classes

**O(1) - Constant time**: The operation takes the same time regardless of input size. Looking up a value in a Python dictionary (hash table) by key is O(1). This is as good as it gets.

**O(log n) - Logarithmic**: Runtime grows slowly as input grows. Binary search on a sorted array is O(log n): doubling the input adds only one more operation. Finding a clip in a sorted list of 1,000,000 clips takes at most 20 comparisons. Vector database approximate nearest-neighbor search is effectively O(log n) due to indexing structures like HNSW.

**O(n) - Linear**: Runtime grows proportionally to input size. Scanning every element in a list once is O(n). Processing every frame in a video once is O(n) where n is the frame count.

**O(n log n) - Linearithmic**: The complexity of efficient sorting algorithms (quicksort, mergesort, Timsort). Sorting 10,000 clips takes roughly 130,000 operations. This is the practical lower bound for comparison-based sorting.

**O(n^2) - Quadratic**: Runtime grows as the square of input size. A naive algorithm that compares every pair of elements is O(n^2). Processing 10,000 video frames with an O(n^2) algorithm takes 100,000,000 operations - 770 times more than O(n log n).

## Why This Matters for AI

The practical difference between complexity classes becomes dramatic at scale:

| n | O(log n) | O(n) | O(n log n) | O(n^2) |
|---|----------|------|------------|--------|
| 100 | 7 | 100 | 664 | 10,000 |
| 10,000 | 13 | 10,000 | 132,877 | 100,000,000 |
| 1,000,000 | 20 | 1,000,000 | 19,931,568 | 10^12 |

**Video processing**: A 30-fps video has 108,000 frames per hour. Any O(n^2) operation over all frames becomes infeasible. The solution is either to avoid quadratic algorithms or to reduce n through sampling and tiered filtering before applying expensive analysis.

**Model inference**: Transformer attention is technically O(n^2) in sequence length, where n is the number of tokens. This is why long-context models are more expensive per token than short-context inference, and why chunking strategies for RAG matter.

**RAG retrieval**: Naive nearest-neighbor search over a vector store is O(n) per query - you scan every vector and compute similarity. With proper indexing (HNSW, IVF), this becomes approximately O(log n), enabling fast retrieval from millions of vectors.

## Amortized Complexity

Some operations are expensive occasionally but cheap on average. Python list `append()` is amortized O(1): most appends are O(1), but occasionally the list must be resized (O(n)). The total cost of n appends is O(n), so the average is O(1).

This matters when analyzing pipeline throughput: an operation that is occasionally slow may not be a bottleneck if it is rare enough.

## Space Complexity

Big-O also applies to memory. Mergesort is O(n log n) time but O(n) space - it needs extra memory proportional to input size. An in-place sort is O(1) space. When loading large datasets into memory for AI training, space complexity determines whether an operation is feasible on available hardware.

## Source

- Cormen, T. H., Leiserson, C. E., Rivest, R. L., and Stein, C. *Introduction to Algorithms* (4th ed., 2022). MIT Press. https://mitpress.mit.edu/9780262046305/

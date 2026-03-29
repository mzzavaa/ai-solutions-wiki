---
title: "RAG Evaluation"
description: "Methods and metrics for measuring the quality of Retrieval Augmented Generation systems, covering retrieval accuracy, generation faithfulness, and end-to-end relevance."
date: 2026-03-28
categories: [Glossary]
tags: [rag, evaluation, metrics, quality, retrieval, generation]
related:
  - glossary/rag
  - guides/rag-evaluation-guide
  - patterns/rag-implementation
  - guides/building-rag-systems
  - guides/llm-evaluation-methods
---

RAG evaluation is the systematic measurement of how well a Retrieval Augmented Generation system performs across its two core functions: retrieving relevant documents and generating accurate, grounded responses. Because RAG systems have multiple components that can fail independently, evaluation must assess each stage and the system as a whole.

## Retrieval Metrics

**Context precision** measures what fraction of retrieved documents are actually relevant to the query. Low precision means the model receives irrelevant noise that can degrade response quality. **Context recall** measures what fraction of all relevant documents were successfully retrieved. Low recall means the model lacks information needed for a complete answer. **Mean Reciprocal Rank (MRR)** evaluates whether relevant documents appear near the top of retrieval results, which matters because models weight earlier context more heavily.

## Generation Metrics

**Faithfulness** (also called groundedness) measures whether the generated response is supported by the retrieved context. A response that introduces claims not found in the retrieved documents is unfaithful, even if factually correct. **Answer relevance** measures whether the response actually addresses the question asked. **Completeness** assesses whether the response covers all aspects of the query that are answerable from the retrieved context.

## End-to-End Metrics

**Answer correctness** compares the generated response against a ground truth answer, often using both semantic similarity and factual overlap. **Hallucination rate** tracks how often the system generates claims unsupported by either the retrieved context or factual reality.

## Evaluation Approaches

**LLM-as-judge** uses a separate language model to score responses on dimensions like faithfulness, relevance, and completeness. Frameworks like RAGAS, DeepEval, and TruLens automate this approach. **Human evaluation** remains the gold standard for subjective quality but is expensive and slow. **Golden datasets** provide pre-built question-answer-context triples for regression testing. **A/B testing** compares system variants in production with real user interactions.

## Continuous Evaluation

RAG systems degrade over time as source documents change, user query patterns shift, and embedding models are updated. Production RAG systems need continuous evaluation pipelines that monitor retrieval and generation quality on live traffic and alert when metrics drift below acceptable thresholds.

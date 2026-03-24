---
title: "RAG - Retrieval Augmented Generation"
description: "What RAG is, how it works, when to use it, and the common implementation pitfalls that reduce retrieval quality."
date: 2026-03-24
categories: [Glossary]
tags: [RAG, retrieval, vector-search, knowledge-base, embeddings]
---

Retrieval Augmented Generation (RAG) is an architecture pattern that improves the accuracy and relevance of AI-generated responses by providing the model with relevant source documents at query time, rather than relying solely on knowledge learned during training.

## How It Works

A RAG system has three phases:

**Indexing (offline)** - Your knowledge source (documents, FAQs, product data, internal wiki) is processed and stored in a vector database. Each document or document chunk is converted to a high-dimensional numerical vector (an embedding) that captures its semantic meaning. Similar content ends up close together in vector space.

**Retrieval (at query time)** - When a user asks a question, that question is also converted to an embedding using the same model. The vector database performs a similarity search to find the chunks whose embeddings are most similar to the question embedding - these are the most likely relevant source documents.

**Generation (at query time)** - The retrieved documents are added to the prompt sent to the language model, along with the original question and an instruction to answer using the provided context. The model generates a response grounded in the retrieved sources.

## When to Use RAG

RAG is the right pattern when:
- The answer depends on private, proprietary, or frequently updated information that is not in the model's training data
- You need answers with citations or source attribution
- Accuracy on factual questions is critical and hallucination must be minimized
- The knowledge base is too large to fit in a single prompt context window

RAG is not the right pattern when:
- The question requires complex multi-step reasoning over the retrieved information (consider fine-tuning or agents)
- The knowledge base is very small and changes infrequently (a few static documents can simply be included in every prompt)
- Retrieval quality cannot be validated and errors in retrieval would be worse than no retrieval

## Implementation Patterns

**Chunk size matters** - Documents are split into chunks before embedding. Chunks too large lose retrieval precision (the relevant sentence is buried in a large block of irrelevant text). Chunks too small lose context (a sentence pulled from the middle of a paragraph may be ambiguous without surrounding context). 300-500 token chunks with 50-100 token overlap between adjacent chunks is a good starting point for most document types.

**Embedding model selection** - The embedding model determines retrieval quality. Specialized embedding models (Cohere Embed, Amazon Titan Embeddings) generally outperform general-purpose LLM-derived embeddings for search tasks. Test with a representative sample of your actual queries before committing to an embedding model.

**Hybrid search** - Pure vector search misses exact keyword matches. Hybrid search combines vector similarity with BM25 (keyword-based) scoring. For most enterprise knowledge bases, hybrid retrieval outperforms pure vector search, particularly for queries containing specific terms, product codes, or proper nouns.

**Re-ranking** - A re-ranker model takes the top N retrieved chunks and re-orders them by relevance to the specific query. This adds latency but significantly improves the quality of context provided to the generation model. Cohere Rerank and cross-encoder models are common choices.

## Common Pitfalls

**Poor chunking strategy** - Splitting documents mid-sentence or mid-table produces chunks that are meaningless in isolation. Implement semantic chunking (split at natural boundaries like paragraphs or section headers) rather than pure token-count chunking.

**Retrieving irrelevant chunks** - If your similarity threshold is too permissive, the model receives irrelevant context that either confuses the answer or (worse) causes it to generate an incorrect answer grounded in the wrong source. Monitor retrieval precision during development and set a minimum similarity threshold.

**Not attributing sources** - A RAG system that does not return source references with its answers removes the ability for users to verify responses. Always include source metadata in the retrieval output and include it in the response.

**Stale index** - If your source documents are updated but the vector index is not refreshed, the system returns outdated information confidently. Implement incremental indexing tied to your document update workflow.

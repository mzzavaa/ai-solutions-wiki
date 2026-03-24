---
title: "Amazon Bedrock - Enterprise AI Foundation"
description: "A comprehensive reference for Amazon Bedrock: available models, key features, use cases, and pricing patterns for enterprise teams."
date: 2026-03-24
categories: [Tools]
tags: [amazon-bedrock, AWS, foundation-models, agents, guardrails, knowledge-bases]
---

Amazon Bedrock is AWS's managed service for foundation model access. It provides a single API to call multiple large language models from different providers, alongside managed infrastructure for knowledge bases, agents, and output safety controls. For enterprise teams building on AWS, it is the primary integration point for generative AI capabilities.

## Available Models

Bedrock provides access to models from several providers. Model availability varies by region.

**Anthropic Claude** - The strongest general-purpose models available on Bedrock. Claude 3.5 Sonnet offers the best balance of capability and cost for most enterprise tasks. Claude 3 Haiku is the fastest and cheapest option for high-volume, simpler tasks. Claude 3 Opus handles the most complex reasoning requirements. Particularly strong for: document analysis, long-context tasks, code generation, structured output extraction.

**Meta Llama** - Open-weights models (Llama 3.1 8B, 70B, 405B; Llama 3.2 1B, 3B, 11B, 90B). Useful when cost is the primary constraint and task complexity is moderate. The 8B model is competitive with older GPT-3.5 class models at a fraction of the cost.

**Amazon Titan** - Amazon's proprietary models. Titan Text is a competent general-purpose model with strong AWS ecosystem integration. Titan Embeddings is well-suited for vector search applications, particularly when used with Bedrock Knowledge Bases.

**Mistral AI** - Mistral 7B, Mistral 8x7B, Mistral Large. European AI provider with a strong compliance story relevant to GDPR and EU AI Act contexts. Competitive performance on instruction-following and summarization tasks.

**Cohere** - Command and Embed models. Cohere's embedding models are particularly strong for semantic search. Command R and Command R+ are optimized for RAG and tool-use workflows.

## Key Features

**Knowledge Bases** - Managed RAG infrastructure. You provide documents (stored in S3), Bedrock handles chunking, embedding, and vector storage. At query time, Bedrock retrieves relevant chunks and augments the prompt. Reduces the infrastructure overhead of building RAG pipelines from scratch. Supports multiple vector stores including OpenSearch Serverless and Aurora PostgreSQL pgvector.

**Agents** - Managed agent runtime. Define actions (Lambda functions, API calls, knowledge base queries) and Bedrock handles the reasoning loop: the model decides which action to take, executes it, processes the result, and continues until the task is complete. Human-in-the-loop patterns are supported via the agent's approval mechanism.

**Guardrails** - Output safety and compliance controls. Configure topic filters (block specified subjects), content filters (harmful content categories with adjustable thresholds), sensitive data redaction (PII detection and masking), and grounding checks (detect hallucinations relative to a provided source document). Guardrails apply to both inputs and outputs and work with any Bedrock model.

**Model evaluation** - Built-in tooling to compare model outputs across a test set. Useful for selecting models and measuring prompt improvements quantitatively rather than through manual review.

## Pricing Patterns

Bedrock uses on-demand pricing (per input/output token) for most use cases, with Provisioned Throughput as an option for guaranteed capacity. On-demand pricing ranges from approximately 0.0003 EUR per 1,000 input tokens (Titan Text Lite) to 0.015 EUR per 1,000 input tokens (Claude 3.5 Sonnet) in eu-west-1. Output tokens are priced 3-5x higher than input tokens.

Cross-region inference (where Bedrock routes requests to the most available region) can improve throughput during peak demand without additional configuration.

For workloads over 40-50 API calls per minute sustained, Provisioned Throughput provides cost predictability. For spiky or low-volume workloads, on-demand is almost always the right choice.

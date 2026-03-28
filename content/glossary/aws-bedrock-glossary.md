---
title: "Amazon Bedrock"
description: "What Amazon Bedrock is, how it provides foundation models as a managed service, and how it enables enterprise generative AI applications on AWS."
date: 2026-03-28
categories: [Glossary]
tags: [AWS, bedrock, foundation-models, generative-AI, LLM, managed-AI, serverless]
related:
  - glossary/foundation-models
  - glossary/llm
  - glossary/rag
  - glossary/guardrails
  - glossary/fine-tuning
---

Amazon Bedrock is a fully managed service that provides access to foundation models (FMs) from multiple AI companies through a single API. It enables developers to build generative AI applications without managing model infrastructure, handling model hosting, scaling, and security within the AWS environment.

## Origins and History

AWS announced Amazon Bedrock in April 2023 during a special announcement event, positioning it as the primary way to access foundation models within the AWS ecosystem. The service reached general availability on September 28, 2023, with an announcement describing five generative AI innovations aimed at making it easier for organizations to "build new generative AI applications, enhance employee productivity, and transform businesses."

At GA launch, Bedrock offered models from AI21 Labs, Anthropic (Claude), Cohere, Stability AI, and Amazon (Titan), with Meta's Llama models following shortly after. The serverless architecture meant customers had no infrastructure to provision -- they made API calls and paid per token.

At re:Invent 2023 (November/December), AWS announced significant expansions: access to Anthropic's Claude 2.1 with a 200,000-token context window, general availability of Agents for Amazon Bedrock (enabling multi-step task execution using company systems and data), and the introduction of Guardrails for Amazon Bedrock (allowing companies to define content filtering policies). Subsequent re:Invent cycles in 2024 and 2025 added Amazon's own Nova model family, Bedrock Knowledge Bases for RAG, reranking capabilities, and model evaluation tools.

## How It Works

**Model access** -- Bedrock provides a unified API (the `InvokeModel` and `Converse` APIs) that abstracts the differences between model providers. Developers can switch between Anthropic Claude, Meta Llama, Mistral, Cohere, and Amazon Titan models by changing a model ID parameter, without modifying application logic. This multi-model access is Bedrock's core value proposition: it avoids vendor lock-in to any single model provider.

**Serverless execution** -- There are no instances to provision or manage. Bedrock handles model hosting, auto-scaling, and high availability. Billing is based on input and output tokens processed (on-demand pricing) or through Provisioned Throughput for workloads requiring guaranteed capacity and consistent latency.

**Knowledge Bases** implement the RAG pattern as a managed service. Developers point Bedrock at data sources (S3, web crawlers, Confluence, SharePoint), and the service handles document chunking, embedding generation, vector storage (in OpenSearch Serverless, Aurora, or Pinecone), and retrieval at query time.

**Agents** allow foundation models to execute multi-step tasks by connecting to APIs and data sources. An agent interprets user requests, breaks them into steps, calls defined action groups (backed by Lambda functions or API schemas), and synthesizes results. This enables use cases like booking travel, processing claims, or querying databases through natural language.

**Guardrails** provide configurable content filtering, denied topic detection, sensitive information redaction (PII), and hallucination detection (contextual grounding checks). Guardrails apply consistently across all models used within an application.

## Enterprise Considerations

**Security** -- All data processed through Bedrock remains within the customer's AWS account and is not used to train base models. Data is encrypted in transit and at rest. VPC endpoints enable private connectivity without internet exposure.

**Fine-tuning and customization** -- Bedrock supports continued pre-training and fine-tuning on customer data, with the customized model hosted securely within the customer's environment. Model evaluation tools allow systematic comparison of model performance on custom benchmarks.

**Cost management** -- On-demand pricing varies significantly across models and modalities. Provisioned Throughput provides predictable costs for production workloads. Batch inference reduces costs for non-time-sensitive processing by up to 50%.

## Sources

1. About Amazon. "Amazon Bedrock General Availability Generative AI Innovations." September 28, 2023. [https://www.aboutamazon.com/news/aws/aws-amazon-bedrock-general-availability-generative-ai-innovations](https://www.aboutamazon.com/news/aws/aws-amazon-bedrock-general-availability-generative-ai-innovations)
2. About Amazon. "AWS Announces More Model Choice and Powerful New Capabilities in Amazon Bedrock." November 2023. [https://press.aboutamazon.com/2023/11/aws-announces-more-model-choice-and-powerful-new-capabilities-in-amazon-bedrock-to-securely-build-and-scale-generative-ai-applications](https://press.aboutamazon.com/2023/11/aws-announces-more-model-choice-and-powerful-new-capabilities-in-amazon-bedrock-to-securely-build-and-scale-generative-ai-applications)
3. AWS Blog. "Top announcements of AWS re:Invent 2023." [https://aws.amazon.com/blogs/aws/top-announcements-of-aws-reinvent-2023/](https://aws.amazon.com/blogs/aws/top-announcements-of-aws-reinvent-2023/)
4. AWS Documentation. "Amazon Bedrock." [https://docs.aws.amazon.com/bedrock/](https://docs.aws.amazon.com/bedrock/)

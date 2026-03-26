---
title: "Programming Languages for AI - Python, TypeScript, HCL, and When to Use Each"
description: "A practical guide to the languages used in AI development: Python for models and agents, TypeScript for frontends and infrastructure, HCL for Terraform, and SQL for data."
date: 2026-03-26
categories: [Guides]
tags: [guides, programming, python, typescript, terraform, fundamentals]
related:
  - glossary/object-oriented-programming
  - glossary/api
  - guides/aws-bedrock-101
  - tools/crewai
---

AI systems rarely live in a single language. A production AI pipeline might use Python to call Bedrock, TypeScript to render the output as video, HCL to provision the infrastructure, and SQL to query the source data. Understanding which language belongs where - and why - is fundamental to building maintainable AI systems.

## Python: The AI-Native Language

Python has become the lingua franca of AI and machine learning. This is not accidental: the language prioritizes readability and rapid prototyping over raw performance, which aligns well with the iterative nature of AI development.

**Core strengths for AI:**

- **Library ecosystem**: PyTorch, TensorFlow, Hugging Face Transformers, LangChain, CrewAI, the AWS Bedrock SDK (boto3), LlamaIndex, and virtually every AI framework has a Python-first implementation.
- **Readability**: Python's syntax is close to pseudocode. Sharing a pipeline with a collaborator who is not a full-time engineer is realistic.
- **REPL and notebooks**: Jupyter notebooks enable exploratory AI development - you run a cell, see results, and iterate. This workflow is poorly supported in compiled languages.
- **Rapid prototyping**: An agent that would take days to build in Java can be tested in Python in hours.

**Weaknesses:**

- **Speed**: Python is interpreted and significantly slower than C++, Rust, or Go for CPU-bound tasks. ML frameworks work around this by calling into C/C++ extensions (PyTorch's backend is C++).
- **The GIL**: The Global Interpreter Lock prevents true CPU parallelism in a single Python process. Workarounds exist (multiprocessing, async IO), but they add complexity.
- **Deployment complexity**: Shipping Python to production requires managing virtual environments, dependency conflicts, and sometimes heavy Docker images.

**Where Python is used**: All model training and fine-tuning, agent frameworks (CrewAI, LangChain, Strands), Bedrock API calls, data preprocessing, AWS Lambda functions for AI pipelines, Rekognition and Transcribe integrations.

Documentation: https://docs.python.org/3/

## TypeScript: Type-Safe JavaScript

TypeScript is JavaScript with static types. It compiles to JavaScript and runs in browsers and Node.js. TypeScript has become the default for serious frontend and full-stack development.

**Core strengths:**

- **Type system**: TypeScript catches type errors at compile time rather than runtime. For AI applications that process structured outputs from models, this matters - a Bedrock response parsed into a TypeScript interface will fail loudly if the structure changes, rather than silently propagating wrong data.
- **Tooling**: Autocompletion, refactoring, and documentation are dramatically better than in plain JavaScript because the type system gives editors full information about what exists.
- **Browser and Node runtime**: TypeScript runs everywhere JavaScript runs. Building a web interface for an AI tool, a Remotion video rendering job, or a CDK infrastructure definition all use the same language.
- **AWS CDK**: The AWS Cloud Development Kit uses TypeScript (and Python) to define infrastructure as code. CDK constructs are TypeScript classes - this is OOP applied to infrastructure.

**Weaknesses:**

- **Not native to ML**: There is no TypeScript equivalent of PyTorch. Running ML inference from TypeScript means calling an API (like Bedrock) or using a small subset of ONNX/TensorFlow.js, which covers only simple models.
- **Build step required**: TypeScript must be compiled to JavaScript before running, adding build tooling complexity.
- **Type system complexity**: TypeScript's type system is expressive but can become arcane. Overengineered type definitions are a common failure mode.

**Where TypeScript is used**: Remotion video templates (React components that render to MP4), Next.js web applications, AWS CDK infrastructure definitions, browser-based AI interfaces.

Documentation: https://www.typescriptlang.org/docs/

## HCL/Terraform: Infrastructure as Declarations

HCL (HashiCorp Configuration Language) is the language of Terraform, the dominant infrastructure-as-code tool. It is not a general-purpose language - it is a declarative configuration format designed specifically to describe infrastructure resources.

**Core strengths:**

- **Declarative**: You describe the desired state of infrastructure, not the steps to get there. Terraform determines what needs to be created, modified, or destroyed.
- **Plan/apply cycle**: `terraform plan` shows exactly what will change before anything happens. This makes infrastructure changes reviewable and auditable.
- **State management**: Terraform tracks what it has created in a state file, enabling it to manage resources across their full lifecycle.
- **Provider ecosystem**: Terraform providers exist for AWS, GCP, Azure, GitHub, Datadog, and hundreds of other services.

**Weaknesses:**

- **Limited logic**: HCL supports conditionals and loops, but complex logic quickly becomes unreadable. For dynamic infrastructure, AWS CDK (Python or TypeScript) is often clearer.
- **Not a programming language**: HCL cannot call APIs, run functions, or do arbitrary computation. It describes resources, not procedures.
- **State file management**: The Terraform state file is a critical artifact. Loss or corruption requires careful recovery.

**Where HCL is used**: Provisioning AWS infrastructure (S3 buckets, Lambda functions, SQS queues, IAM roles, VPCs), declaring ECS task definitions, setting up DynamoDB tables and Bedrock endpoints.

Documentation: https://developer.hashicorp.com/terraform/docs

## SQL: The Language of Data

SQL (Structured Query Language) is the universal language for querying relational databases and, increasingly, data warehouses. AI pipelines almost always have an upstream data source that SQL queries.

**Where SQL is used**: Querying source data for AI training, retrieving records for RAG pipelines, storing structured AI outputs (scores, classifications, metadata), analytics on AI pipeline results.

## Linda Mohamed's Language Stack

Linda Mohamed uses Python for all AI and agent work: Bedrock API calls, CrewAI agents, Rekognition and Transcribe integrations, AWS Lambda pipeline logic. TypeScript is her choice for Remotion video templates (which are React components) and Next.js web applications. All AWS infrastructure is defined in HCL with Terraform.

This separation is deliberate: each language does what it is best at. Python handles the intelligence layer, TypeScript handles the presentation layer, and HCL handles the infrastructure layer. They communicate through APIs and S3 artifacts rather than sharing codebases.

## Choosing the Right Language

| Task | Language |
|------|----------|
| AI model inference | Python (boto3/Bedrock SDK) |
| Agent frameworks | Python (CrewAI, LangChain, Strands) |
| Video rendering | TypeScript (Remotion) |
| Web UI | TypeScript (Next.js, React) |
| AWS infrastructure | HCL (Terraform) or TypeScript (CDK) |
| Data queries | SQL |
| High-performance inference server | C++, Rust, or Go |

## Sources

- Python Software Foundation. *Python 3 Documentation*. https://docs.python.org/3/
- Microsoft. *TypeScript Documentation*. https://www.typescriptlang.org/docs/
- HashiCorp. *Terraform Documentation*. https://developer.hashicorp.com/terraform/docs

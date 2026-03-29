---
title: "Model Registry"
description: "What a model registry is, how it provides versioned storage and lifecycle management for trained ML models, and why it is essential for production ML."
date: 2026-03-28
categories: [Glossary]
tags: [model-registry, mlops, model-versioning, model-management, deployment, governance]
related:
  - glossary/mlops
  - glossary/experiment-tracking
  - glossary/model-card
  - patterns/model-versioning
  - tools/mlflow
  - guides/model-registry-guide
---

A model registry is a centralized repository that stores trained ML model artifacts along with their metadata, version history, and lifecycle state. It serves as the single source of truth for which models exist, which version is deployed to each environment, and the lineage and evaluation results associated with every version.

## The Problem It Solves

Without a model registry, model artifacts live in ad-hoc locations: S3 buckets with inconsistent naming, local directories on data scientists' machines, or embedded in pipeline outputs with no metadata attached. Teams lose track of which model version is in production, cannot reproduce previous versions, and have no systematic way to compare candidates for promotion.

## Core Capabilities

**Version management** - Each model is registered under a name with sequential version numbers. Every version has an immutable artifact (the serialized model weights and code) and associated metadata.

**Lifecycle stages** - Models progress through defined stages: development, staging, production, and archived. The registry tracks which version is in each stage and who promoted it.

**Metadata and lineage** - Each version records its training run ID, evaluation metrics, training data version, code commit, hyperparameters, and any other metadata needed for reproducibility and auditing.

**Access control** - Role-based permissions determine who can register models, who can promote them between stages, and who can deploy them. This enforces governance: a data scientist can register a model but only a reviewer or automated pipeline can promote it to production.

**Artifact storage** - The registry either stores model artifacts directly or provides references to artifacts in external storage, with integrity checks (hashes) to ensure artifacts have not been modified.

## How It Fits in the ML Lifecycle

Experiment tracking captures every training run. The best runs are registered in the model registry as candidate versions. Validation pipelines evaluate candidates against the current production model. Approved candidates are promoted to the production stage. The deployment system reads the production model from the registry and serves it. The registry provides the handoff point between model development and model deployment.

## Tools

Common model registry implementations include MLflow Model Registry, Amazon SageMaker Model Registry, Vertex AI Model Registry, and Azure ML Model Registry. MLflow's open-source registry is widely adopted and integrates with most ML frameworks and deployment platforms.

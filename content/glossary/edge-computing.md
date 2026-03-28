---
title: "Edge Computing"
description: "What edge computing is, how it brings computation closer to data sources, and when edge deployment is appropriate for AI workloads."
date: 2026-03-28
categories: [Glossary]
tags: [edge-computing, IoT, latency, CDN, inference]
related:
  - glossary/cdn
  - glossary/serverless
  - glossary/inference
---

Edge computing processes data near its source - at the network edge, on devices, or in local facilities - rather than sending all data to a centralized cloud data center. This reduces latency, conserves bandwidth, and enables operation when network connectivity is unreliable or unavailable.

## How It Works

Instead of sending raw data to the cloud for processing, edge computing deploys compute resources close to where data is generated. These edge resources run inference models, filter data, make real-time decisions, and send only relevant results or aggregated data to the cloud.

**AWS edge services** span a spectrum from CDN-based compute (CloudFront Functions, Lambda@Edge) to local hardware (AWS Outposts, Snow Family devices, IoT Greengrass). The choice depends on how close to the data source you need processing and how much compute is required.

## Why It Matters for AI

**Latency-critical inference** - autonomous vehicles, industrial robotics, and real-time video analysis cannot tolerate the round-trip latency of cloud inference. Running models at the edge enables sub-millisecond response times.

**Bandwidth constraints** - sending all video frames from thousands of cameras to the cloud for analysis is impractical. Edge inference processes video locally and sends only events or metadata.

**Offline operation** - manufacturing floors, remote locations, and mobile deployments need AI capabilities even when cloud connectivity is intermittent.

**Data sovereignty** - some regulations require data to remain within specific geographic boundaries. Edge processing keeps data local.

## Practical Considerations

Edge deployment constrains model size and compute. Models must be optimized (quantized, pruned, distilled) to run on edge hardware with limited memory and no GPU. Model updates require over-the-air deployment mechanisms with rollback capability.

The common pattern is a hybrid architecture: lightweight models run at the edge for real-time decisions, while the cloud handles training, model updates, complex analysis, and long-term storage. AWS IoT Greengrass supports deploying and managing ML models on edge devices with this hybrid pattern.

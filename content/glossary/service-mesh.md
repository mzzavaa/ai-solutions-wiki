---
title: "Service Mesh"
description: "What a service mesh is, how it manages service-to-service communication, and when the complexity is justified."
date: 2026-03-28
categories: [Glossary]
tags: [service-mesh, istio, microservices, observability, networking]
related:
  - glossary/sidecar-pattern
  - glossary/kubernetes
  - glossary/istio
---

A service mesh is an infrastructure layer that manages service-to-service communication in a microservices architecture. It handles traffic routing, load balancing, encryption, authentication, observability, and retry logic between services without requiring changes to application code. The mesh operates transparently through sidecar proxies deployed alongside each service instance.

## How It Works

Each service instance gets a sidecar proxy (typically Envoy) that intercepts all inbound and outbound network traffic. These proxies handle mutual TLS encryption, retries, circuit breaking, load balancing, and traffic routing. A control plane (Istio, Linkerd, AWS App Mesh) configures the proxies with routing rules and policies.

The application code communicates as if talking directly to other services. The sidecar proxy transparently adds security, reliability, and observability features to every request.

## Why It Matters

In a microservices architecture with tens or hundreds of services, implementing retry logic, circuit breaking, mutual TLS, and distributed tracing in every service is impractical and error-prone. A service mesh moves these concerns out of application code and into infrastructure, ensuring consistent behavior across all services regardless of language or framework.

For AI platforms with multiple microservices (inference endpoints, feature stores, orchestrators, post-processing services), a service mesh provides unified observability, traffic management, and security.

## When to Use a Service Mesh

A service mesh adds significant operational complexity. It is justified when you have many (20+) microservices, strong security requirements (mutual TLS everywhere), complex traffic management needs (canary deployments, traffic splitting), or when consistent observability across services is critical.

It is not justified for small numbers of services, monolithic applications, or teams without Kubernetes expertise. The operational overhead of managing the mesh infrastructure is real and ongoing.

## Practical Guidance

Start without a service mesh and add one when communication complexity becomes a bottleneck. If you do adopt a mesh, choose based on your infrastructure: AWS App Mesh for ECS-based deployments, Istio or Linkerd for Kubernetes. Invest in understanding the proxy's resource overhead (CPU, memory, latency) and plan capacity accordingly.

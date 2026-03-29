---
title: "CDN - Content Delivery Network"
description: "What CDNs do, how CloudFront accelerates content delivery, and when to use a CDN for AI application frontends."
date: 2026-03-28
categories: [Glossary]
tags: [CDN, CloudFront, caching, performance, edge-computing]
related:
  - glossary/edge-computing
  - glossary/api-gateway
---

A Content Delivery Network (CDN) is a globally distributed network of servers (edge locations) that caches and delivers content from locations physically close to end users. By reducing the distance between the user and the server, CDNs decrease latency, improve load times, and reduce load on origin servers.

## How It Works

When a user requests content, the CDN routes the request to the nearest edge location. If the edge has a cached copy (cache hit), it serves the content immediately. If not (cache miss), the edge fetches the content from the origin server, serves it to the user, and caches it for subsequent requests.

**Amazon CloudFront** is AWS's CDN service with 400+ edge locations worldwide. It integrates with S3 (static assets), ALB/EC2 (dynamic content), API Gateway (API responses), and Lambda@Edge/CloudFront Functions (edge compute).

## Why It Matters

For AI-powered applications, the frontend (HTML, JavaScript, CSS, images) should be served from a CDN for fast global load times. Static assets like model visualizations, documentation, and pre-computed results are ideal CDN content. Even dynamic API responses can benefit from short-TTL caching when many users make similar queries.

CDNs also provide DDoS protection (absorbing attack traffic at the edge), SSL/TLS termination (reducing origin server load), and request compression.

## Practical Guidance

Place CloudFront in front of S3 for all static assets. For AI application APIs, consider caching responses for common queries with short TTLs (seconds to minutes) to reduce backend inference load and improve response times.

Configure appropriate cache behaviors: long TTLs for immutable assets (hashed filenames), short TTLs for dynamic content, and no caching for personalized or real-time responses. Use origin access control to ensure S3 content is only accessible through CloudFront, not directly from the S3 bucket URL.

Monitor cache hit ratio to measure CDN effectiveness. A low hit ratio suggests TTLs are too short, caching rules need adjustment, or the content is too personalized for effective caching.

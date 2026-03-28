---
title: "Site Reliability Engineering (SRE)"
description: "What SRE is, how it applies software engineering to operations, and key SRE practices for AI platform reliability."
date: 2026-03-28
categories: [Glossary]
tags: [SRE, reliability, operations, DevOps, error-budget]
related:
  - glossary/error-budget
  - glossary/sla-slo-sli
  - glossary/toil
  - glossary/observability
---

Site Reliability Engineering (SRE) is a discipline that applies software engineering practices to infrastructure and operations. Originated at Google, SRE treats operations as a software problem: automating manual work, defining reliability targets with error budgets, and balancing feature velocity against system stability through principled engineering practices.

## Core Practices

**Service Level Objectives (SLOs)** define reliability targets based on what users actually need, not arbitrary uptime percentages. SLOs drive decisions about when to invest in reliability versus features.

**Error budgets** quantify acceptable unreliability. If your SLO allows 0.1% error rate, you have an error budget of 0.1%. When the budget is consumed (too many errors), feature releases pause and the team focuses on reliability. When there is budget remaining, the team ships features faster.

**Toil reduction** systematically identifies and automates repetitive, manual operational work. If a human is doing work that a machine could do, SRE principles say to automate it.

**Blameless postmortems** analyze incidents to improve systems, not to assign blame. The goal is learning and prevention, not punishment.

## Why It Matters

SRE provides a framework for making reliability decisions objectively rather than politically. Instead of debating whether the system is "reliable enough," teams measure SLIs against SLOs and use error budgets to make data-driven decisions about priorities.

For AI platforms, SRE practices are essential because AI systems have unique reliability challenges: model degradation over time, non-deterministic behavior, long inference latencies, and complex failure modes that traditional monitoring may miss.

## Practical Guidance

Start with SLOs - define what "reliable" means for your AI service from the user's perspective (inference latency under 2 seconds for 99% of requests, availability of 99.9%). Instrument your system to measure SLIs accurately. Calculate error budgets monthly. When the budget is spent, shift priorities to reliability work. Identify your top sources of toil and automate the highest-impact ones first. You do not need a dedicated SRE team to adopt SRE practices - any engineering team can start with SLOs and error budgets.

---
title: "Auto-Scaling"
description: "What auto-scaling is, how it adjusts capacity dynamically, and how to configure scaling policies for cost-efficient AI workloads."
date: 2026-03-28
categories: [Glossary]
tags: [auto-scaling, elasticity, cost-optimization, EC2, ECS]
related:
  - glossary/load-balancer
  - glossary/serverless
  - glossary/kubernetes
---

Auto-scaling automatically adjusts the number of compute resources (EC2 instances, ECS tasks, DynamoDB capacity, SageMaker endpoints) based on demand. When load increases, auto-scaling adds capacity. When load decreases, it removes excess capacity. This matches resources to actual demand, avoiding both over-provisioning (wasting money) and under-provisioning (degrading performance).

## How It Works on AWS

**EC2 Auto Scaling** adjusts the number of EC2 instances in an Auto Scaling group. You define minimum, maximum, and desired capacity, plus scaling policies that determine when to add or remove instances.

**ECS Service Auto Scaling** adjusts the number of ECS tasks (containers) running in a service. Works with both Fargate and EC2 launch types.

**Application Auto Scaling** provides auto-scaling for other AWS services: DynamoDB table capacity, SageMaker endpoint instances, Aurora replicas, and Lambda provisioned concurrency.

## Scaling Policies

**Target tracking** maintains a specified metric at a target value. For example, "keep average CPU at 60%" or "keep request count per target at 100." The simplest and most commonly used policy type.

**Step scaling** adds or removes a specified number of instances when a CloudWatch alarm fires. Offers more control than target tracking but requires more configuration.

**Scheduled scaling** adjusts capacity at specific times. Useful for predictable patterns: scale up before business hours, scale down at night.

**Predictive scaling** uses machine learning to forecast demand and pre-scale capacity before load arrives. Reduces the lag between demand increase and capacity availability.

## Practical Guidance for AI Workloads

AI inference workloads often have variable demand. Configure target tracking on request latency or queue depth rather than CPU utilization, since inference latency is what users experience. Set conservative scale-in policies (slower cooldown) to avoid thrashing during fluctuating loads. For batch AI processing, use scheduled scaling or event-driven scaling with SQS queue depth as the trigger.

Always set a maximum capacity limit to prevent runaway costs from unexpected traffic spikes or retry loops.

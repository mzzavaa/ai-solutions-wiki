---
title: "Adversarial Machine Learning"
description: "How evasion, poisoning, and model extraction attacks threaten ML systems, and the defenses available to mitigate them."
date: 2026-03-28
categories: [Glossary]
tags: [adversarial-ML, security, evasion-attacks, data-poisoning, model-robustness]
related:
  - glossary/ai-safety
  - glossary/ai-red-team
  - glossary/prompt-injection
  - glossary/guardrails
---

Adversarial machine learning studies how attackers can manipulate ML systems and how to defend against such attacks. Unlike traditional software security, which focuses on code vulnerabilities, adversarial ML exploits the statistical nature of learned models. Small, carefully crafted perturbations to inputs can cause misclassification, training data manipulation can corrupt model behavior, and external queries can steal model functionality.

## How It Works

**Evasion attacks** modify inputs at inference time to cause misclassification. Adversarial examples add imperceptible perturbations to images that fool classifiers (a stop sign misclassified as a speed limit sign) or modify text to bypass content filters. Methods like FGSM, PGD, and C&W generate adversarial examples by optimizing perturbations to maximize the model's loss.

**Poisoning attacks** corrupt training data to manipulate model behavior. Backdoor attacks insert triggered patterns (e.g., a small patch in training images) that cause specific misclassifications when the trigger is present at inference time, while performing normally on clean inputs. Data poisoning can also degrade overall model accuracy by introducing mislabeled or adversarial training examples.

**Model extraction attacks** use query access to a deployed model to train a surrogate model that replicates its behavior. An attacker sends carefully chosen inputs, collects predictions, and trains a copy. This threatens proprietary models, as the extracted model can be used to generate adversarial examples or to avoid API costs.

## Why It Matters

As ML systems are deployed in safety-critical and security-sensitive contexts (autonomous driving, malware detection, financial fraud prevention, content moderation), adversarial vulnerabilities become a direct business and safety risk. Understanding these threats is essential for risk assessment and compliance, particularly as AI regulations increasingly require robustness testing.

## Practical Considerations

Defense starts with threat modeling: identify which attack types are realistic for your deployment. Adversarial training (including adversarial examples during training) is the most established defense against evasion attacks. Input preprocessing, certified defenses, and ensemble methods add additional layers. For model extraction, implement rate limiting, query monitoring, and watermarking. For poisoning, invest in data provenance and validation. Tools like IBM ART, Foolbox, and CleverHans support adversarial robustness evaluation. Include adversarial testing in your ML deployment pipeline alongside standard accuracy metrics.

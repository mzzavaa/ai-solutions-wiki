---
title: "Terraform"
description: "What Terraform is, how HashiCorp's declarative infrastructure tool works, the design of HCL, and the state management model that enables infrastructure as code at scale."
date: 2026-03-28
categories: [Glossary]
tags: [terraform, infrastructure-as-code, HCL, HashiCorp, DevOps, IaC]
related:
  - glossary/infrastructure-as-code-glossary
  - glossary/gitops
  - glossary/immutable-infrastructure
---

Terraform is an open-source infrastructure as code tool created by Mitchell Hashimoto and Armon Dadgar at HashiCorp. It allows operators to define cloud and on-premises infrastructure in declarative configuration files that can be versioned, reviewed, and reused across teams.

## Origins and History

Mitchell Hashimoto first recognized the need for a cloud-agnostic infrastructure provisioning tool in 2011, when AWS released CloudFormation. The day after that launch, Hashimoto published a blog post arguing that an open-source, provider-neutral alternative was needed and invited the community to build one. When no one did, HashiCorp built it themselves.

On July 28, 2014, HashiCorp released Terraform 0.1 with support for AWS and DigitalOcean. The announcement described Terraform as "a tool for safely and efficiently building, combining, and launching infrastructure." The initial vision was to compose resources across multiple providers -- servers from AWS, DNS from CloudFlare, databases from Heroku -- and build them all in parallel.

Terraform was far from an overnight success. Downloads were largely stagnant for the first eighteen months, and the team considered shutting the project down. By late 2016, however, the provider ecosystem had grown to over 750 contributors and dozens of providers including Azure, Google Cloud, and OpenStack. Downloads began doubling monthly in 2017. Terraform 1.0 reached general availability in June 2021, signaling production stability. In April 2024, IBM announced the acquisition of HashiCorp for $6.4 billion, closing in February 2025.

## How It Works

Terraform uses a declarative approach: operators describe the desired end state of infrastructure rather than the steps to reach it. The tool calculates the difference between the current state and the desired state, then generates an execution plan showing exactly what will be created, modified, or destroyed.

**HashiCorp Configuration Language (HCL)** is Terraform's domain-specific language. HCL was designed to be human-readable while remaining machine-parseable, sitting between JSON (too verbose for humans) and YAML (too ambiguous for complex logic). HCL supports variables, expressions, conditional logic, and iteration, enabling reusable infrastructure modules.

**Providers** are plugins that translate HCL declarations into API calls for specific platforms. The Terraform Registry hosts thousands of providers covering major cloud platforms, SaaS services, and internal tools. This provider architecture is what makes Terraform genuinely multi-cloud rather than cloud-agnostic in name only.

**State management** is central to Terraform's operation. Terraform maintains a state file that maps declared resources to real-world infrastructure objects. This state file records resource IDs, dependency relationships, and metadata. When Terraform plans changes, it compares the configuration against state, not against the live infrastructure directly. Remote state backends (S3, Terraform Cloud, Consul) allow teams to share state safely with locking to prevent concurrent modifications.

## Key Concepts

**Plan and Apply** -- Terraform separates planning from execution. `terraform plan` previews changes without modifying anything. `terraform apply` executes the plan. This two-phase workflow enables code review of infrastructure changes before they reach production.

**Modules** are reusable packages of Terraform configuration. A module encapsulates a set of related resources (for example, a VPC with subnets, route tables, and security groups) behind a clean input/output interface. The Terraform Registry hosts community and verified modules.

**Workspaces** allow a single configuration to manage multiple environments (development, staging, production) with different variable values and separate state files.

## Limitations

Terraform's state file introduces operational complexity. State drift occurs when infrastructure is modified outside of Terraform. State file corruption or loss can require manual intervention to recover. Large state files slow planning operations, and state locking failures can block team workflows.

The August 2023 license change from MPL 2.0 to the Business Source License (BSL 1.1) prompted the community fork OpenTofu under the Linux Foundation, fragmenting the ecosystem.

## Sources

1. HashiCorp. "Terraform Announcement." July 28, 2014. [https://www.hashicorp.com/en/blog/terraform-announcement](https://www.hashicorp.com/en/blog/terraform-announcement)
2. HashiCorp. "The Story of HashiCorp Terraform with Mitchell Hashimoto." [https://www.hashicorp.com/en/resources/the-story-of-hashicorp-terraform-with-mitchell-hashimoto](https://www.hashicorp.com/en/resources/the-story-of-hashicorp-terraform-with-mitchell-hashimoto)
3. HashiCorp. "Announcing HashiCorp Terraform 1.0 General Availability." June 2021. [https://www.hashicorp.com/en/blog/announcing-hashicorp-terraform-1-0-general-availability](https://www.hashicorp.com/en/blog/announcing-hashicorp-terraform-1-0-general-availability)
4. "Terraform (software)." Wikipedia. [https://en.wikipedia.org/wiki/Terraform_(software)](https://en.wikipedia.org/wiki/Terraform_(software))

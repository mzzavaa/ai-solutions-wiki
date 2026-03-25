---
title: "Terraform - Infrastructure as Code for AI Projects"
description: "Using Terraform to provision and manage AWS infrastructure for AI projects: modular design, state management, and multi-environment patterns."
date: 2026-03-24
categories: [Tools]
tags: [terraform, IaC, infrastructure, AWS, DevOps]
---

Terraform is an infrastructure-as-code tool that provisions cloud resources from declarative configuration files. You describe the desired state of infrastructure in HCL (HashiCorp Configuration Language), Terraform computes the difference from the current state, and applies the changes. For AI projects on AWS, Terraform manages everything from S3 buckets and Lambda functions to Bedrock configurations and IAM roles.

Official documentation: https://www.terraform.io/

## Core Concepts

**Providers** are plugins that map Terraform resources to cloud API calls. The AWS provider covers all AWS services. A provider block configures the AWS region and authentication:

```hcl
provider "aws" {
  region = var.aws_region
}
```

**Resources** declare infrastructure objects. Each resource block maps to a single cloud resource:

```hcl
resource "aws_s3_bucket" "ai_pipeline_input" {
  bucket = "${var.project_name}-input-${var.environment}"
}
```

**Variables** parameterize configurations. Separate variable files per environment (`dev.tfvars`, `prod.tfvars`) keep environment differences explicit and reviewable.

**Outputs** export values (ARNs, URLs, IDs) from one module to be referenced by another.

## State Management

Terraform tracks the current state of provisioned infrastructure in a **state file** (`terraform.tfstate`). For teams, store state in S3 with DynamoDB locking:

```hcl
terraform {
  backend "s3" {
    bucket         = "my-terraform-state"
    key            = "ai-pipeline/prod.tfstate"
    region         = "eu-west-1"
    dynamodb_table = "terraform-locks"
  }
}
```

Never commit state files to version control - they contain sensitive values (ARNs, database endpoints) and cause merge conflicts.

## Module Design for AI Projects

Modules are reusable Terraform packages. A well-structured AI project might have modules:

- `modules/ai-pipeline/` - S3 buckets, Lambda functions, Step Functions, EventBridge rules
- `modules/auth/` - Cognito User Pool, Identity Pool, IAM roles
- `modules/search/` - OpenSearch Serverless collection and access policies

Each environment (`environments/dev/`, `environments/prod/`) calls the modules with environment-specific variables. This keeps environment configuration minimal while sharing the resource definitions.

## Multi-Environment Pattern

```
environments/
  dev/
    main.tf      # calls modules
    dev.tfvars   # dev-specific values
  prod/
    main.tf
    prod.tfvars
modules/
  ai-pipeline/
    main.tf
    variables.tf
    outputs.tf
```

Deploy to dev with `terraform apply -var-file=dev.tfvars`. Promote to prod after validation.

## Terraform vs AWS CDK

The primary trade-off: Terraform is multi-cloud and uses its own DSL (HCL); CDK is AWS-only but uses familiar programming languages (Python, TypeScript). See the [Terraform vs CDK comparison]({{< relref "terraform-vs-cdk.md" >}}) for a detailed breakdown.

## Related Articles

- [Infrastructure as Code]({{< relref "/glossary/infrastructure-as-code.md" >}}) - concept overview
- [Terraform vs CDK]({{< relref "terraform-vs-cdk.md" >}}) - choosing between IaC tools
- [Serverless Computing]({{< relref "/glossary/serverless.md" >}}) - infrastructure Terraform manages

---
title: "AWS Amplify"
description: "What AWS Amplify is, how it evolved from a JavaScript library to a full-stack serverless framework, and how Gen 2 introduced a TypeScript-first development model."
date: 2026-03-28
categories: [Glossary]
tags: [AWS, amplify, serverless, full-stack, frontend, TypeScript, hosting]
related:
  - glossary/aws-cognito-glossary
  - glossary/aws-lambda-glossary
  - glossary/aws-s3-glossary
  - glossary/serverless
---

AWS Amplify is a set of tools and services for building full-stack web and mobile applications on AWS. It abstracts the complexity of provisioning and configuring backend services -- authentication, APIs, storage, hosting -- behind a developer-friendly interface, allowing frontend developers to build cloud-connected applications without deep AWS expertise.

## Origins and History

AWS introduced Amplify in November 2017 at AWS re:Invent as an open-source JavaScript library designed to simplify the integration of mobile and web applications with AWS backend services. At launch, even adding a basic login page required wrestling with CloudFormation templates and IAM policies. Amplify aimed to collapse that boilerplate into simple library calls.

The platform evolved rapidly through a series of milestones. In August 2018, the Amplify CLI launched as a command-line tool that generated backend resources through an interactive wizard, automatically creating least-privilege IAM roles, Cognito user pools, API Gateway endpoints, and S3 buckets. In November 2018, Amplify Console (now Amplify Hosting) introduced Git-based continuous deployment with automatic branch previews.

In December 2020, Amplify Studio (initially called Admin UI) provided a visual interface for building backends without the CLI. A 2021 update added Figma-to-React code generation, enabling designers to export components directly into Amplify applications.

**Amplify Gen 2**, previewed at re:Invent 2023 and reaching general availability in 2024, represents a fundamental architectural shift. Gen 2 replaces the CLI wizard and JSON configuration files with a TypeScript-first, code-first approach. Developers define their backend resources -- authentication rules, data models, storage buckets, functions -- entirely in TypeScript using the Amplify libraries. This configuration is stored alongside application code in the repository, enabling standard code review, version control, and refactoring workflows.

## How It Works

**Authentication** -- Amplify integrates with Amazon Cognito to provide user sign-up, sign-in, multi-factor authentication, and social identity federation. In Gen 2, authentication rules are defined in TypeScript with type-safe configuration for OAuth providers, user attributes, and MFA settings.

**Data** -- Amplify provides a GraphQL API layer backed by AWS AppSync and DynamoDB. Developers define their data model using a schema, and Amplify generates the API, database tables, and client-side code for queries, mutations, and real-time subscriptions.

**Storage** -- File storage is backed by Amazon S3, with access rules defined per user, per group, or publicly. Amplify provides client libraries for upload, download, and access control.

**Hosting** -- Amplify Hosting provides CI/CD from Git repositories with automatic branch deployments, pull request previews, and custom domain management. It supports static sites, server-side rendered frameworks (Next.js, Nuxt), and single-page applications.

**Functions** -- Serverless functions backed by AWS Lambda can be defined and deployed as part of the Amplify project, handling custom business logic, API routes, or event-driven processing.

## Gen 2 Architecture

Gen 2 uses AWS Cloud Development Kit (CDK) under the hood. When developers define resources in TypeScript, Amplify translates those definitions into CDK constructs, which synthesize into CloudFormation templates for deployment. This means Amplify Gen 2 applications benefit from the full power of CloudFormation while developers interact with a higher-level abstraction.

A per-developer sandbox environment gives each team member an isolated cloud backend tied to their Git branch, enabling parallel development without environment conflicts.

## Sources

1. AWS Blog. "AWS Amplify Evolution Timeline -- 2017 to 2025." [https://dev.to/aws-builders/aws-amplify-evolution-timeline-2017-to-2025-d83](https://dev.to/aws-builders/aws-amplify-evolution-timeline-2017-to-2025-d83)
2. AWS Blog. "Introducing the Next Generation of AWS Amplify's Fullstack Development Experience." [https://aws.amazon.com/blogs/mobile/introducing-amplify-gen2/](https://aws.amazon.com/blogs/mobile/introducing-amplify-gen2/)
3. AWS Documentation. "AWS Amplify." [https://docs.amplify.aws/](https://docs.amplify.aws/)
4. Collins, F. "AWS Amplify 2024: A New Era." [https://blog.focusotter.com/aws-amplify-in-2024-is-not-the-amplify-you-grew-up-with](https://blog.focusotter.com/aws-amplify-in-2024-is-not-the-amplify-you-grew-up-with)

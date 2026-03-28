---
title: "AWS Lambda"
description: "What AWS Lambda is, how Tim Wagner's event-driven compute service launched the serverless paradigm, and how the execution model works under the hood."
date: 2026-03-28
categories: [Glossary]
tags: [AWS, lambda, serverless, functions, event-driven, compute]
related:
  - glossary/serverless
  - glossary/event-driven-architecture
  - glossary/aws-cognito-glossary
  - glossary/api-gateway
---

AWS Lambda is a serverless compute service that runs code in response to events without requiring the provisioning or management of servers. Developers upload function code, configure triggers, and AWS handles execution, scaling, and availability. Billing is per invocation and per millisecond of compute time, with no charge for idle capacity.

## Origins and History

AWS Lambda was announced at AWS re:Invent 2014 by Dr. Tim Wagner, who had joined AWS in 2012 and conceived the service. In a 2013 meeting, Jeff Barr and Wagner discussed ways to let developers focus on code rather than infrastructure. Barr later recalled "throwing my arms skyward and indicating that it would be cool to simply toss the code into the air and have the cloud grab, store, and run it." Wagner wrote an internal PRFAQ proposing exactly that, and Lambda was greenlit -- sponsored by the S3 team and approved by Andy Jassy.

At re:Invent 2014, Werner Vogels introduced Lambda in the Day 2 keynote, and Wagner presented session MBL202, "Getting Started with AWS Lambda," with a live demo. The preview launch supported only Node.js, with functions limited to 60 seconds of runtime, 25 concurrent executions per account, and 128 MB to 1 GB of configurable memory. Lambda was initially positioned as "a kind of simple scripting mechanism to thumbnail images coming into S3."

Wagner's original pitch was for an event-driven glue service, not a general-purpose compute platform. He reportedly asserted that no one would ever use it for video transcoding -- a prediction that proved wrong. Wagner later wrote on the AWS Compute Blog that "you could use AWS Lambda to build entirely serverless applications," coining one of the earliest uses of the term "serverless" in this context. Austen Collins, creator of the Serverless Framework, cited that blog post as the first time he encountered the word.

## How It Works

**Functions** are the unit of deployment. A function consists of code (uploaded as a ZIP archive or container image), a runtime (Node.js, Python, Java, Go, .NET, Ruby, or a custom runtime), a handler entry point, and configuration (memory, timeout, environment variables, IAM execution role).

**Triggers** invoke functions. Lambda integrates with over 200 AWS services and event sources: S3 object creation, DynamoDB stream records, API Gateway HTTP requests, SQS messages, EventBridge rules, Kinesis data streams, SNS notifications, and many more. Each event source provides a JSON event payload that Lambda passes to the function handler.

**Execution model** -- When a function is invoked, Lambda provisions a lightweight execution environment (a microVM managed by Firecracker, an open-source VMM that AWS built for Lambda and Fargate). If a warm environment from a previous invocation is available, Lambda reuses it, avoiding cold start latency. If not, a new environment is initialized (cold start), which includes downloading the code, starting the runtime, and running initialization code outside the handler.

**Scaling** is automatic. Lambda creates new execution environments in response to concurrent invocations, scaling from zero to thousands of instances without configuration. Each AWS account has a default concurrency limit (typically 1,000 concurrent executions per region, adjustable), and reserved concurrency can guarantee capacity for critical functions.

## Key Capabilities

**Provisioned concurrency** pre-initializes a specified number of execution environments, eliminating cold starts for latency-sensitive workloads. **Lambda@Edge** and **CloudFront Functions** run code at AWS edge locations for low-latency request processing. **Lambda Layers** provide shared code and dependencies across multiple functions. **Container image support** (added December 2020) allows functions packaged as OCI container images up to 10 GB, enabling complex dependency trees and existing container-based workflows.

## Constraints

Functions have a maximum execution timeout of 15 minutes (increased from the original 60 seconds). The maximum memory allocation is 10 GB, which also determines proportional CPU allocation. The deployment package size limit is 50 MB zipped (250 MB unzipped) for ZIP archives, or 10 GB for container images. These constraints mean Lambda is not suitable for all workloads -- long-running batch processing, persistent connections, and GPU-intensive tasks require alternative compute models.

## Sources

1. AWS Blog. "AWS Lambda turns ten -- looking back and looking ahead." November 2024. [https://aws.amazon.com/blogs/aws/aws-lambda-turns-ten-the-first-decade-of-serverless-innovation/](https://aws.amazon.com/blogs/aws/aws-lambda-turns-ten-the-first-decade-of-serverless-innovation/)
2. AWS Compute Blog. "Compute content at re:Invent 2014." [https://aws.amazon.com/blogs/compute/reinvent2014/](https://aws.amazon.com/blogs/compute/reinvent2014/)
3. Serverless Chats Podcast. "Episode #52: The Past, Present, and Future of Serverless with Tim Wagner." [https://www.serverlesschats.com/52/](https://www.serverlesschats.com/52/)
4. Lober, F. "10 Years of AWS Lambda -- The Evolution, Impact, and Future of Serverless." Medium. [https://medium.com/@fabian_lober/10-years-of-aws-lambda-the-evolution-impact-and-future-of-serverless-1-2-0da1e86a9dae](https://medium.com/@fabian_lober/10-years-of-aws-lambda-the-evolution-impact-and-future-of-serverless-1-2-0da1e86a9dae)

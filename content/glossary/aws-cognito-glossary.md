---
title: "Amazon Cognito"
description: "What Amazon Cognito is, how identity pools and user pools differ, and how it implements OAuth 2.0 and OpenID Connect for application authentication."
date: 2026-03-28
categories: [Glossary]
tags: [AWS, cognito, authentication, OAuth, OIDC, identity, serverless]
related:
  - glossary/aws-amplify-glossary
  - glossary/aws-lambda-glossary
  - glossary/api-gateway
  - glossary/serverless
---

Amazon Cognito is a fully managed identity service that provides user authentication, authorization, and user management for web and mobile applications. It handles the complete authentication lifecycle -- sign-up, sign-in, password recovery, multi-factor authentication, and token management -- without requiring developers to build or manage identity infrastructure.

## Origins and History

Amazon Cognito became generally available on July 10, 2014. The original announcement described it as "a simple user identity and data synchronization service that helps you securely manage and synchronize app data for your users across their mobile devices." At launch, Cognito supported identity federation through Amazon, Facebook, and Google login providers, as well as unauthenticated guest access. The initial feature set also included device data synchronization, allowing application state (preferences, game progress) to be stored in the AWS Cloud and synced across devices.

In the months following launch, Cognito expanded rapidly. In September 2014, developer authenticated identities were introduced, allowing applications with their own user databases to obtain temporary AWS credentials. In October 2014, OpenID Connect support was added, opening federation to any OIDC-compliant identity provider.

A pivotal evolution came in 2016 with the introduction of Cognito User Pools, which transformed Cognito from a federation and sync service into a complete identity provider. User Pools added a managed user directory with sign-up and sign-in flows, password policies, email and phone verification, and a hosted authentication UI.

## Identity Pools vs. User Pools

This distinction is the most important architectural concept in Cognito and the most common source of confusion.

**User Pools** are user directories. A User Pool stores user accounts, handles registration and authentication, and issues JSON Web Tokens (JWTs) -- an ID token, access token, and refresh token. User Pools are an OpenID Connect identity provider. They manage usernames, passwords, user attributes, MFA, and account recovery. When an application needs to know who a user is, it uses a User Pool.

**Identity Pools** (also called Federated Identities) map authenticated users to temporary AWS credentials (IAM roles). An Identity Pool does not store users or handle authentication itself. It accepts tokens from a User Pool, a social provider (Google, Apple, Facebook), a SAML provider, or an OIDC provider, and exchanges them for scoped AWS credentials. When an application needs a user to access AWS resources directly (S3 buckets, DynamoDB tables, API Gateway endpoints secured with IAM), it uses an Identity Pool.

The typical architecture uses both: User Pools handle authentication and issue tokens, then Identity Pools exchange those tokens for AWS credentials with fine-grained permissions based on the user's identity or group membership.

## OAuth 2.0 and OIDC Implementation

Cognito User Pools implement the OAuth 2.0 authorization framework and the OpenID Connect protocol. The hosted UI provides standard OAuth endpoints: `/authorize`, `/token`, `/userInfo`, and `/logout`. Supported grant types include the authorization code grant (recommended for server-side and mobile applications), the implicit grant (legacy, for SPA applications), and client credentials (for machine-to-machine communication).

Cognito supports custom scopes through resource servers, allowing fine-grained access control beyond the standard `openid`, `email`, and `profile` scopes. Lambda triggers enable custom logic at key points in the authentication flow: pre-sign-up validation, custom authentication challenges, pre-token generation for claim enrichment, and post-confirmation side effects.

## Limitations

Cognito has hard limits that affect architecture decisions: 40,000 requests per second per User Pool (soft limit, can be increased), a maximum of 10,000 app clients per User Pool, and a maximum of 25 custom attributes per user. Token customization is limited compared to dedicated identity platforms -- modifying claims requires Lambda triggers, adding latency and complexity.

## Sources

1. AWS. "Introducing Amazon Cognito." July 10, 2014. [https://aws.amazon.com/about-aws/whats-new/2014/07/10/introducing-amazon-cognito/](https://aws.amazon.com/about-aws/whats-new/2014/07/10/introducing-amazon-cognito/)
2. AWS. "Latest Amazon Cognito Features." November 6, 2014. [https://aws.amazon.com/about-aws/whats-new/2014/11/06/latest-amazon-cognito-features/](https://aws.amazon.com/about-aws/whats-new/2014/11/06/latest-amazon-cognito-features/)
3. Konishi, H. "AWS History and Timeline regarding Amazon Cognito." [https://hidekazu-konishi.com/entry/aws_history_and_timeline_amazon_cognito.html](https://hidekazu-konishi.com/entry/aws_history_and_timeline_amazon_cognito.html)
4. AWS Documentation. "Amazon Cognito." [https://docs.aws.amazon.com/cognito/](https://docs.aws.amazon.com/cognito/)

---
title: "GitHub Actions"
description: "What GitHub Actions is, how its YAML-based workflow system and composable actions model work, and how it became the dominant CI/CD platform for open-source projects."
date: 2026-03-28
categories: [Glossary]
tags: [github-actions, CI-CD, DevOps, automation, workflows, GitHub]
related:
  - glossary/ci-cd
  - glossary/gitops
  - glossary/feature-branching
  - glossary/trunk-based-development
---

GitHub Actions is a CI/CD and workflow automation platform built directly into GitHub. It allows developers to define event-driven workflows in YAML files that run on GitHub-hosted or self-hosted runners, triggered by repository events such as pushes, pull requests, issue creation, or scheduled cron expressions.

## Origins and History

GitHub announced Actions in limited public beta at GitHub Universe on October 16, 2018, in San Francisco. The announcement positioned Actions not as a traditional CI/CD pipeline product but as a general-purpose workflow automation system built on open-source principles. At launch, workflows were defined in a custom HCL-like syntax, and each action step ran inside a Docker container on GitHub's servers.

Industry analyst James Governor of RedMonk described the Universe 2018 launch as "low key revolutionary," noting that GitHub was embracing and extending CI/CD. The announcement was immediately seen as a competitive threat to established CI services such as CircleCI and Travis CI, which had built their businesses on tight GitHub integration.

Between the beta and general availability, GitHub made a significant design change: the workflow definition format was switched from HCL to YAML, aligning with the configuration language already familiar to most DevOps practitioners. GitHub Actions reached general availability at Universe 2019 in November, with full CI/CD capabilities including matrix builds, artifact storage, and caching.

## How It Works

**Workflows** are YAML files stored in `.github/workflows/` within a repository. Each workflow defines one or more jobs, and each job runs on a specified runner (Ubuntu, Windows, macOS, or self-hosted). Jobs run in parallel by default but can declare dependencies to enforce sequential execution.

**Events** trigger workflows. GitHub supports dozens of event types: `push`, `pull_request`, `schedule` (cron), `workflow_dispatch` (manual), `release`, `issue_comment`, and more. This event-driven model means workflows respond to the full lifecycle of software development, not just code changes.

**Actions** are the composable building blocks of workflows. An action is a reusable unit of automation packaged as a GitHub repository. Actions can be written in JavaScript (running directly on the runner) or as Docker containers (running in isolation). The GitHub Marketplace hosts thousands of community-contributed actions for common tasks: setting up language runtimes, deploying to cloud providers, sending notifications, running security scans.

**The composability model** is GitHub Actions' defining architectural decision. Rather than building a monolithic CI system with every feature built in, GitHub designed a minimal core (event triggers, runners, job orchestration) and delegated specific functionality to community-authored actions. This means the platform's capabilities grow with the ecosystem rather than with GitHub's own engineering investment.

## Key Features

**Matrix builds** allow a single job definition to run across multiple combinations of operating systems, language versions, and configuration parameters. A matrix strategy can test a library against Node 18, 20, and 22 on Ubuntu and macOS simultaneously.

**Secrets and environments** provide secure storage for credentials, with environment-level protection rules such as required reviewers and wait timers before deployment proceeds.

**Reusable workflows** (introduced in 2021) allow an entire workflow file to be called from another workflow, enabling organizations to standardize CI/CD patterns across hundreds of repositories from a single source of truth.

**Self-hosted runners** allow organizations to run workflows on their own infrastructure when GitHub-hosted runners do not meet security, compliance, or performance requirements.

## Sources

1. GitHub Blog. "GitHub Actions: built by you, run by us." October 17, 2018. [https://blog.github.com/2018-10-17-action-demos/](https://blog.github.com/2018-10-17-action-demos/)
2. Governor, J. "GitHub Universe 2018: Low Key Revolutionary." RedMonk. November 7, 2018. [https://redmonk.com/jgovernor/2018/11/07/github-universe-2018-low-key-revolutionary/](https://redmonk.com/jgovernor/2018/11/07/github-universe-2018-low-key-revolutionary/)
3. InfoQ. "GitHub Release Developer Workflow Tools: Actions, Suggested Changes & Security Alerts." October 2018. [https://www.infoq.com/news/2018/10/github-universe-2018-actions/](https://www.infoq.com/news/2018/10/github-universe-2018-actions/)
4. GitHub Blog. "New from Universe 2019: GitHub for mobile, GitHub Archive Program, and more." November 2019. [https://github.blog/news-insights/product-news/universe-day-one/](https://github.blog/news-insights/product-news/universe-day-one/)

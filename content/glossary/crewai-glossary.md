---
title: "CrewAI"
description: "CrewAI is an open-source Python framework for orchestrating role-based autonomous AI agents, created by Joao Moura in 2023."
date: 2026-03-28
categories: [Glossary]
tags: [crewai, multi-agent, ai-agents, orchestration, framework]
related:
  - glossary/multi-agent-orchestration
  - glossary/multi-agent-systems
  - glossary/ai-agents
  - glossary/agentic-ai
---

CrewAI is an open-source Python framework for orchestrating multiple autonomous AI agents that collaborate to complete complex tasks. Each agent is assigned a specific role, a set of tools, and a goal. CrewAI handles the orchestration: passing context between agents, managing tool calls, handling retries on failure, and collecting the final output. The framework was created by Joao Moura and released as an open-source project on GitHub in late 2023.

## Origins and History

Joao Moura built the initial prototype of CrewAI while experimenting with a small agent to help him write LinkedIn posts more efficiently [1]. That experiment revealed a broader insight: the barrier to building and deploying multi-agent systems was unnecessarily high. Moura finished building the framework in October 2023 and quietly released it as an open-source project on GitHub the following month [2]. The project gained rapid traction, accumulating tens of thousands of GitHub stars within months.

In January 2024, CrewAI incorporated as a company with Moura as CEO and Rob Bailey as COO. The company attracted 150 enterprise customers within its first six months and raised funding from investors who were themselves CrewAI users. By 2025, CrewAI reported powering over 1.4 billion agentic automations across enterprise customers including PwC, IBM, Capgemini, and NVIDIA [3].

## Core Abstractions

CrewAI is organized around three primary abstractions that mirror how human teams work.

**Agents** are autonomous units with a defined role, a backstory providing context, and a goal. Each agent has access to specific tools (web search, file I/O, API calls, code execution) and an LLM that powers its reasoning. An agent might be a "Senior Research Analyst" with access to web search and document retrieval, or a "Technical Writer" with access to a file system and a style guide.

**Tasks** define discrete units of work with a description, expected output format, and an assigned agent. Tasks can specify dependencies on other tasks, creating execution order.

**Crews** are collections of agents and tasks that work together. The crew defines the overall process: sequential (tasks execute in order), hierarchical (a manager agent delegates to workers), or custom (developer-defined orchestration logic). When a crew is kicked off, CrewAI manages the execution flow, passing outputs from completed tasks as context to downstream tasks.

## Role-Based Agent Collaboration Pattern

CrewAI's distinctive contribution is formalizing the role-based collaboration pattern for AI agents. Rather than building a single monolithic agent that attempts to handle all aspects of a complex task, CrewAI encourages decomposing the work into specialized roles. This mirrors organizational design: a research team has analysts, writers, and reviewers, each with distinct expertise and responsibilities.

This pattern produces better results than single-agent approaches for several reasons. Each agent's prompt can be focused and specific, reducing ambiguity. Tool access can be scoped to what each role needs, reducing error surface. And the output of each agent can be validated before passing it downstream.

## Comparison with Alternatives

CrewAI is one of three major multi-agent orchestration frameworks. Microsoft's AutoGen (2023) uses a conversational pattern where agents communicate through message passing. LangGraph, part of the LangChain ecosystem, provides a lower-level graph-based abstraction for defining agent workflows. CrewAI is the most opinionated of the three, providing higher-level abstractions that trade flexibility for faster development of common patterns.

CrewAI is built entirely from scratch and is independent of LangChain or other agent frameworks, though it can integrate with various LLM providers and tool ecosystems.

## Sources

1. Moura, J. (2023). Twitter post on CrewAI origins. [https://x.com/joaomdmoura/status/1933162425869861101](https://x.com/joaomdmoura/status/1933162425869861101)
2. CrewAI GitHub Repository. [https://github.com/crewAIInc/crewAI](https://github.com/crewAIInc/crewAI)
3. Insight Partners (2025). "How CrewAI is orchestrating the next generation of AI Agents." [https://www.insightpartners.com/ideas/crewai-scaleup-ai-story/](https://www.insightpartners.com/ideas/crewai-scaleup-ai-story/)
4. IBM. "What is CrewAI?" [https://www.ibm.com/think/topics/crew-ai](https://www.ibm.com/think/topics/crew-ai)

---
title: "Infrastructure as Code (IaC) - History and Concepts"
description: "The origins and evolution of Infrastructure as Code, from Mark Burgess's CFEngine in 1993 through Puppet, Chef, and Ansible to modern Terraform and CDK."
date: 2026-03-28
categories: [Glossary]
tags: [infrastructure-as-code, IaC, CFEngine, Puppet, Chef, Ansible, terraform, CDK, DevOps]
related:
  - glossary/terraform-glossary
  - glossary/gitops
  - glossary/immutable-infrastructure
  - glossary/infrastructure-as-code
---

Infrastructure as Code (IaC) is the practice of managing and provisioning computing infrastructure through machine-readable definition files rather than manual configuration or interactive tools. IaC treats infrastructure -- servers, networks, load balancers, databases, DNS records -- as software artifacts that can be versioned, tested, reviewed, and deployed through the same workflows used for application code.

## Origins and History

The concept of automated infrastructure configuration traces back to 1993, when Mark Burgess, a postdoctoral fellow at Oslo University in Norway, created CFEngine. Burgess was tasked with maintaining a collection of Unix workstations in the Department of Theoretical Physics, each running a different Unix variant with different problems. Manual scripting was drowning in platform-specific exception logic. Burgess abstracted the differences behind a domain-specific language that described the desired end state of a system rather than the steps to reach it.

CFEngine introduced the concept of **convergent configuration** -- the idea that configuration operations should be idempotent fixed points. Running CFEngine repeatedly on a system, regardless of its starting state, would always converge to the declared policy-compliant state. This declarative, desired-state model is the intellectual foundation of all modern IaC tools.

Burgess presented CFEngine at the HEPix conference in Paris in 1993. He later developed promise theory, a formal model of distributed cooperation, and incorporated it into CFEngine 3 (2008). Burgess served as professor of Network and System Administration at Oslo University College from 1994 to 2011 -- the first professor with that title.

### The Configuration Management Generation (2005-2012)

CFEngine's ideas influenced a generation of more accessible tools. **Puppet** (2005), created by Luke Kanies, introduced a Ruby-based declarative DSL for configuration management with a client-server architecture and a module ecosystem. **Chef** (2009), co-founded by Adam Jacob, took a programmatic approach using Ruby as the configuration language, giving operators the full power of a general-purpose language. **Ansible** (2012), created by Michael DeHaan, eliminated the need for agents on managed nodes by using SSH for communication and YAML for playbooks, dramatically lowering the adoption barrier.

The term "Infrastructure as Code" gained currency around 2008-2009, coinciding with the DevOps movement. Andrew Clay Shafer and Patrick Debois catalyzed DevOps with a talk at Agile 2008. The first documented uses of the phrase "Infrastructure as Code" appeared in Clay Shafer's "Agile Infrastructure" talk at Velocity 2009 and in John Willis's summary of that talk. Adam Jacob (Chef) and Luke Kanies (Puppet) were using the phrase around the same time.

### The Provisioning Generation (2011-present)

The earlier tools focused on configuring existing servers. AWS CloudFormation (2011) shifted the scope to provisioning infrastructure itself -- creating servers, networks, and services from declarations. **Terraform** (2014), created by Mitchell Hashimoto at HashiCorp, extended this to multiple cloud providers with a single tool and language (HCL), becoming the dominant multi-cloud provisioning tool.

**AWS CDK** (2019) took a different approach: instead of a DSL, developers define infrastructure using general-purpose programming languages (TypeScript, Python, Java, Go) that synthesize into CloudFormation templates. **Pulumi** (2018) applied the same idea across multiple cloud providers, competing with Terraform by offering Python, TypeScript, Go, and C# as alternatives to HCL.

## Declarative vs. Imperative

IaC tools fall on a spectrum. **Declarative** tools (Terraform, CloudFormation, Puppet) describe what the infrastructure should look like; the tool determines how to reach that state. **Imperative** tools (Ansible playbooks, shell scripts) describe the steps to execute. Most modern tools are declarative, though Ansible blends both paradigms -- its playbooks describe tasks to execute, but many modules are internally idempotent.

## Key Principles

**Idempotency** -- Applying the same configuration multiple times produces the same result. This is what makes IaC safe to run repeatedly and what enables drift detection and correction.

**Version control** -- Infrastructure definitions live in Git alongside application code. Changes are proposed via pull requests, reviewed by peers, and tracked in commit history.

**Immutability** -- Rather than modifying servers in place (mutable infrastructure), immutable infrastructure replaces servers entirely on each deployment. New instances are provisioned from a clean image, and old instances are terminated. This eliminates configuration drift.

**Testing** -- Infrastructure code can be validated before deployment through linting (tflint, cfn-lint), policy checks (Open Policy Agent, Sentinel), plan previews (terraform plan), and integration tests that provision and verify real infrastructure.

## Sources

1. Burgess, M. "CFEngine." 1993. [https://en.wikipedia.org/wiki/CFEngine](https://en.wikipedia.org/wiki/CFEngine)
2. Burgess, M. "Mark Burgess (computer scientist)." Wikipedia. [https://en.wikipedia.org/wiki/Mark_Burgess_(computer_scientist)](https://en.wikipedia.org/wiki/Mark_Burgess_(computer_scientist))
3. The New Stack. "A Brief DevOps History: The Roots of Infrastructure as Code." [https://thenewstack.io/a-brief-devops-history-the-roots-of-infrastructure-as-code/](https://thenewstack.io/a-brief-devops-history-the-roots-of-infrastructure-as-code/)
4. Morris, K. *Infrastructure as Code*, 3rd Edition. O'Reilly Media. [https://infrastructure-as-code.com/book/](https://infrastructure-as-code.com/book/)
5. Mike Tyson of the Cloud. "The Origins of Infrastructure as Code: A Brief History of DevOps." Medium. [https://medium.com/@mike_tyson_cloud/the-origins-of-infrastructure-as-code-a-brief-history-of-devops-a883d8877f19](https://medium.com/@mike_tyson_cloud/the-origins-of-infrastructure-as-code-a-brief-history-of-devops-a883d8877f19)

---
layout: post
title: "When Building Becomes Easy, Thinking Gets Harder"
date: 2026-06-25
categories: ai-assisted-development agents engineering
---

*AI-assisted development lowers the cost of creating software, but it raises the cost of choosing the wrong solution.*

A few days ago, I was asked to improve an agent-like task someone had already built and was running locally inside Claude Cowork.

The task was useful. It was not a toy. It solved a real problem, produced real value, and was already part of someone’s workflow.

My first instinct as an engineer was immediate and predictable: this should become a real service.

By “real,” I meant the usual engineering shape: a codebase, a cloud deployment, persistent storage, authentication, background jobs, monitoring, CI/CD, and eventually a proper multi-user operational model. I saw a useful local agent and mentally translated the request into a software architecture problem.

That reaction felt natural. Maybe even responsible. If something is important, we usually want it to be reliable. If it is useful, we start thinking about scale. If multiple people might use it, we imagine a centralized system. If we want to improve it, we tend to think in terms of structure, durability, and productization.

That was my first mental model.

But there was an important detail: I was not thinking about building that service the old way.

I was already using the full power of AI-assisted development: Claude Code, Spec Kit, Superpowers, structured specifications, generated implementation paths, and an increasingly agentic development workflow. The cost of building a cloud service is lower than it used to be. The tooling is faster. The feedback loops are better. The scaffolding is easier. The distance between idea, specification, implementation, and deployment has collapsed dramatically.

That is exactly what made the assumption more subtle.

When AI-assisted development makes it easier to build software, it also becomes easier to overbuild software. The question was no longer whether I could build this as a proper software system efficiently. The answer to that was probably yes. The better question was whether this should become a software system at all.

## The assumption started to break

As I worked through the problem, the real challenge became clearer. The hard part was not primarily Azure, databases, containers, infrastructure, or deployment automation. The hard part was understanding the workflow.

What information actually mattered? How should the Slack context be collected? What did the agent need to know in order to produce a useful result? How should the reasoning be structured? How would the output be consumed? Which parts of the task needed more precision, and which parts needed better judgment?

Even the Slack work was not “old way” engineering. I was not manually poking around in the dark. It was part of an AI-assisted development process: using tools, agents, and structured exploration to understand the data shape, test assumptions, refine the task, and identify the right abstraction.

That changed the direction of the work.

Instead of immediately turning the task into a full cloud product, I explored whether the local Claude Cowork model could be improved first. The question became whether the agent could be better structured, whether the workflow could support more than one person, and whether a two-agent approach could produce a more useful and repeatable result without introducing a full service architecture.

The answer was yes.

The result was a meaningful improvement, but it was not a cloud service. There was no Azure deployment, no database, no container, no Terraform, no Key Vault, no observability stack, and no new backend service to maintain. It was a better local agent architecture running inside the host environment that already existed.

That forced me to ask a more interesting question: why did I assume that “better” meant “more software,” even when AI-assisted development had made the software path easier than ever?

## The old engineering reflex

Engineers are trained to think in systems. That is not a bad thing. It is one of the reasons software works at scale.

We think about reliability, scalability, ownership, state, observability, maintainability, security, compliance, failure modes, and operational control. Those instincts are valuable. They help us avoid fragile solutions, build things that last, and protect users and organizations from invisible complexity.

But those same instincts can also push us too quickly toward heavier architecture.

A local agent can feel temporary. A prompt-based workflow can feel informal. A desktop-hosted agent can feel less “real” than a service running in the cloud. A workflow improvement can feel less serious than a productized platform.

So we reach for the tools we know. We imagine a codebase, a database, a queue, an API, a worker, a deployment pipeline, and monitoring. We take a problem that may be mostly about human workflow, context, judgment, and information synthesis, and we translate it into a software system almost automatically.

That reflex made sense in the world we came from.

But AI-assisted development changes the equation.

## The new risk: AI-accelerated over-engineering

The old version of over-engineering had a natural friction: building a system was expensive. It took time. You had to think carefully before committing to an architecture, because implementation carried a meaningful cost.

AI-assisted development reduces that friction.

Claude Code, Spec Kit, Superpowers, and similar tools make it much faster to move from intention to specification, from specification to code, and from code to a working system. That is powerful, but it also creates a new risk. When building becomes easier, the act of building stops being the main constraint.

**The bigger constraint becomes judgment.**

We need to decide what should become code, what should remain a prompt, what should be an agent workflow, what should stay close to a human, and what actually needs infrastructure, state, tenancy, and operational guarantees.

AI-assisted development does not eliminate architecture. It makes architecture more important, because now we can build the wrong thing faster.

## The real decision is not local versus cloud

At first glance, this story looks like a comparison between a local agent and a cloud service. But I think that framing is too narrow.

The deeper decision is not about where the code runs. It is about the kind of solution the problem needs.

Sometimes we are improving a person’s workflow. Sometimes we are building an operational system. Those are different jobs, and they should not automatically lead to the same architecture.

A local Claude Cowork agent is not necessarily a prototype or a shortcut. A cloud service is not necessarily the mature version of the same idea. One adds intelligence to a workflow. The other creates a system that operates independently.

Both are valid. But they come with different costs, guarantees, and responsibilities.

## Two architectural paths

This comparison helped me clarify the decision.

| Dimension            | Local Claude Cowork agent path                                            | Full coded service path                                                                     |
| -------------------- | ------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| What it is           | An agent workflow built through prompts, configuration, and orchestration | A software service built with code, SDKs, infrastructure, storage, and deployment pipelines |
| Runtime ownership    | The host owns the runtime                                                 | You own the runtime                                                                         |
| Agent loop           | Managed by Claude Cowork or the host environment                          | Implemented and controlled by your service                                                  |
| Execution model      | Usually human-triggered or host-scheduled                                 | Autonomous, scheduled, event-driven, or continuously running                                |
| State                | Local files, user context, host-managed memory, or lightweight artifacts  | Durable database, queues, storage, audit logs, and server-side history                      |
| Identity and secrets | Uses the user’s already-authorized connectors and local context           | Requires OAuth, token storage, secret management, permissions, and rotation                 |
| Tenancy              | Usually individual or small-group oriented                                | Designed for multiple users, teams, operators, or customers                                 |
| Deployment           | Minimal or none                                                           | Full CI/CD, containers, infrastructure as code, monitoring, and release management          |
| Maintenance          | Mostly prompt and workflow iteration                                      | Full software lifecycle: tests, builds, security scans, dependencies, incident response     |
| Control              | Lower control, but high leverage                                          | Maximum control, but much higher ownership                                                  |
| Best fit             | Workflow augmentation                                                     | Productized system                                                                          |

The core distinction is simple: a local agent is useful when you are adding intelligence to someone’s workflow. A coded service is necessary when you are building an operational system.

That difference matters more than the feature list.

## When the local agent path makes sense

Choose it when **all or most** of these hold:

- **A human is in the loop.** Someone triggers it and acts on the output. The "never send / draft only" posture is the tell — it's advisory, not autonomous.
- **It operates in one person's context** — their accounts, their machine, their data. Per-user, not org-wide.
- **The logic fits in prompts + orchestration.** No heavy parsing, no deterministic business rules you need to unit-test, no performance constraints.
- **You want zero infra and near-zero ops.** No deploy, no secrets, no on-call. Anthropic billing rides on the Cowork subscription.
- **Iteration speed and non-engineer maintainability matter.** A PM can edit a Markdown prompt; they can't edit a Fastify handler.
- **Data should stay local** (privacy/locality as a feature).

The upside is speed and leverage. You can improve the workflow without taking on deployment, databases, auth, observability, or incident response.

The trade-off is that you are borrowing someone else’s runtime. You have less control over execution, state, connectors, failures, and guarantees. That is acceptable for advisory work with human review. It becomes risky when the agent starts acting autonomously or becomes part of a business-critical process.

## When the coded service path makes sense

Choose it when **any** of these are true — these are essentially disqualifiers for the plugin path:

- **It must run autonomously** — continuously, on a schedule, or event-driven, with no human present. (worklens polls Slack 24/7.)
- **Multi-tenant / serves the org** from one deployment, with self-service onboarding.
- **Durable, queryable, auditable state** — a database, transactions, history, reporting.
- **Real-time reaction + reliability engineering** — queues, retries, rate-limit handling, backpressure.
- **A public surface** — OAuth callbacks, webhooks, APIs.
- **Hard guarantees and posture** — SLAs, observability, Key Vault, OIDC, secret scanning, CodeQL, compliance. Things you must *prove*, not assert.
- **Logic that exceeds prompts** — e.g. worklens uses `chrono-node` for deadline parsing, Zod schemas, deterministic dedup. You want that in tested code.
- **Independence** — it must outlive any one person's laptop and not depend on a host app.

The upside is control. You own the runtime, state, agent loop, retries, observability, and operational model.

The trade-off is ownership. You also own uptime, secrets, authentication, permissions, logs, deployment, security posture, dependency updates, support, and the consequences of autonomous behavior.

AI-assisted development can make the service faster to build. It does not make the service free to own.

## The hard part is no longer only building

For a long time, building was expensive enough that it forced discipline. You had to choose carefully because the cost of implementation was high.

Now that cost is falling.

AI-assisted development makes implementation faster, cheaper, and more accessible. It gives us more leverage than we had before. But leverage cuts both ways: it helps us build the right thing faster, and it also helps us build the wrong thing faster.

**So the engineering skill that becomes more valuable is not only the ability to implement. It is the ability to choose the right shape of solution.**

A solution can be a prompt, an agent workflow, a local tool, a spreadsheet, a script, a plugin, a human-in-the-loop process, a full software service, a platform, or a product.

The question is not which one is more impressive. The question is which one matches the problem.

## What I learned

My first instinct was not wrong. It was just incomplete.

The coded service version would make sense if the task needed to run autonomously, support many users centrally, maintain durable shared state, and provide operational guarantees. But that was not necessarily the immediate problem.

The immediate problem was improving the usefulness, structure, and repeatability of a workflow that still lived close to a human operator. For that, a better local Claude Cowork agent was not a compromise. It was the right architectural level.

That is probably the most important lesson for me: engineering maturity is not measured by how much infrastructure we add. It is measured by whether the architecture matches the problem.

## A warning to engineers

We should be careful with the word “real.”

Real does not always mean cloud. It does not always mean database. It does not always mean service, container, queue, dashboard, and deployment pipeline.

And now, with AI-assisted development, we need to be even more careful. The easier it becomes to build a full system, the more disciplined we need to be about deciding whether the system should exist.

Claude Code, Spec Kit, Superpowers, and similar tools can dramatically reduce the cost of implementation. But they do not remove the cost of ownership.

You may build the service faster, but you still own the runtime, secrets, uptime, data persistence, monitoring, retries, failures, and operational consequences of turning a workflow into a system.

A solution is real if it solves the problem with the right level of reliability, cost, control, and complexity.

Sometimes that means Azure, databases, CI/CD, Terraform, monitoring, and a fully coded agent. Sometimes it means a well-designed local agent inside Claude Cowork that makes a person dramatically more effective.

The danger is not just over-engineering. The newer danger is AI-accelerated over-engineering: building the wrong architecture faster than ever.

Before asking, “How do we productionize this?”, ask a different question:

Does this need to be a product, a system, or simply a much better workflow?

![forma logo](/img/forma-logo.svg)



> The **challenge** of Generative AI is that it shines at first but then takes hours of engineering to make it enterprise ready

## What is Forma?

Forma is a framework for building reliable, **production-grade AI agents**. In our experience, some rules of thumb that can help you do this is are:

1. **Maximise prompting time** - Contrary to the specific algorithm and software architecture, every AI Agent requires their own unique prompts. So, spend your time testing, tuning, refine and evaluating prompts, not re-inventing the software.
2. **Agents should be auditable** - As the requirements from clients become more strict, system instructions or prompts can become quite complex and contradictions might leak into them. You and other people should be able to proof-read them.
3. **Evaluate often** - As outlined in the [Evaluation](./evals.md) section, understanding the impact of changing system prompts is not easy. Evaluations need to be part of the workflow.
4. **Reduce iteration time** - When getting an Agent into production, you will make tons of changes in settings, changes in prompts and more. Making this step faster can really accelerate your way to production.
5. **Integrate it with your existing infrastructure** - An AI agent is always a component in a broader system. Therefore, AI Agents should be flexible enough to become part of existing or growing infrastructure.
6. **Monitor** - The variability in inputs to an AI Agent is enormous. This, added to the stochastic nature of their behaviour, means that even if your AI Agent passed all the quality assurance tests, you need to keep a close eye on it.


<div style="width: fit-content; margin:auto; padding: 1em;">
    <a style="padding: 0.5em 1em; border-radius:0.5em; background-color:var(--links); color:white;" href="../forma-docs/how-to/getting-started.md">Jump to "Quick start"</a>
</div>

## How Forma helps you follow the principles above

Forma operates on simple principles that help you avoid mistakes and maintain the higher standards of security.

### 1. Maximise prompting time

Forma's AI Agents are not 'coded', but 'configured' using `yaml`, `json` and `markdown` files. These files have all the information required for Forma's runtime to bring an AI Agent to live.

All of Forma's AI Agents are built using the same [building blocks](./building-blocks.md), making them predictable and easily auditable. The runtime incorporates best-practices which might not be worth re-thinking every time you begin working on a new agent.

Here is a simple example of an AI Agent. (We will explain this in more detail later.)

```yaml
id: the-agent
start:
    nodes:
    - llm:
        provider: ollama
       system_prompt: 'You are a helpful assistant'
```

### 2. Agents should be auditable

A Forma agent fits naturally within a standard code repository (`git`). This means that all prompts, workflows, and configurations are version-controlled and easily auditable. They can follow the same code review and quality assurance standards as the rest of your codebase. 

Additionally, Forma agents are defined using `yaml`, `json` and `markdown` files. This makes them even easier to audit, because most code editors and version-control services (such as Github) do an excellent job at rendering these files in a very readable manner.

> **Note** - Some would argue that using `markdown` files for system prompts is not great because you cannot create prompt templates or chains, and you cannot create reusable 'prompt' blocks. The truth is that that is exactly what we are trying to avoid here, for the following reasons:
> * Contrary to programming code, prompts are not modular. They need to be coherent instructions. You cannot just replace one sentence by another sentence.
> * Having reusable 'blocks' makes it really hard to audit the final prompt, because it is really not written anywhere, just built at runtime.
> 
> [Forma DOES have prompt templates](../how-to/templates.md). However, the placeholders in them is reserved for values created dynamically, at runtime, by LLMs (as opposed to values known at development time).


### 3. Evaluate often

The Forma CLI has built-in evaluation support. You can test the agent as a whole, or the [sub components](./building-blocks.md) independently.

This means you can test both during development, and within CI/CD pipelines.

### 4. Reduce iteration time

The Forma CLI  offers very quick hot reloading that let you iterate quickly without getting out of "the zone". These features streamline iteration and  raise errors early.

### 5. Integrate it with your existing infrastructure

Forma is designed on a simple principle: an AI agent is always a component in a broader system. Every production-grade service—even those powered by AI—relies on databases, logging, authentication, front-ends, and security. 

Therefore, rather than asking you to migrate your workflow to a new hosted platform, Forma is designed to plug directly into your existing stack. Some key design choices that make this possible are:

1. **Version Control:** - As explained earlier, Forma and version control work very well together.
2. **DevOps-Ready CLI:** - The Forma CLI is the primary interface for developing and testing AI agents. It runs consistently on your machine, in production, and in CI/CD pipelines, enabling seamless automation, testing, and deployment.
3. **Container-based** - All production-grade artifacts produced by Forma are Containers that you can deploy wherever you want, with the settings and security measures that your organisation deems appropriate.


> The drawback of this principle design is that Forma **doesn’t come with batteries included**. We know this makes it slightly harder to start and develop (e.g., local development requires running adjacent services); however, it makes it far easier to adapt, extend, and integrate with your organization’s existing systems and compliance requirements.


### 6. Monitor

The container images we give you have built-in [Opentelemetry](https://opentelemetry.io/) instrumentation, with added [Openinference](https://arize-ai.github.io/openinference) standards ([semantic conventions](https://arize-ai.github.io/openinference/spec/semantic_conventions.html)) so you can analise your traces using [Phoenix Arize](https://phoenix.arize.com). This lets you check integrate Forma agents within your existing observability stack.

I am working on adding the Opentelemetry [Generative AI Framework semantic conventions](https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-agent-spans/) as well.
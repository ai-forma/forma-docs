# What is `Forma`?

> The **challenge** of Generative AI is that it shines at first but then takes hours of engineering to make it enterprise ready

Forma is a framework for building reliable, production-grade AI agents and integrating them seamlessly into your existing cloud infrastructure. While opinionated by design, Forma **doesn’t come with batteries included**. That makes it slightly harder to start—but far easier to adapt, extend, and integrate with your organization’s existing systems and compliance requirements.


<div style="width: fit-content; margin:auto; padding: 1em;">
    <a style="padding: 0.5em 1em; border-radius:0.5em; background-color:var(--links); color:white;" href="/how-to/quickstart.md">Jump to "Quick start"</a>
</div>

Forma operates on simple principles that help you avoid mistakes and maintain the higher standards of security.

## 1. Focus on prompting, not coding

Define and manage complex agent logic using simple, version-controlled `yaml` and `markdown` files. Additionally, our developer tools offer quick hot reloading that let you iterate quickly without getting out of "the zone". These features streamline iteration, minimizes coding errors, and allows your prompt engineers and developers to collaborate seamlessly.

Here is a simple example of an AI Agent. (We will explain this in more detail later.)

```yaml
id: the-agent
start:
    nodes:
    - llm:
        provider: ollama
       system_prompt: 'You are a helpful assistant'
```

## 2. Architected for Your Existing Cloud Infrastructure

Forma is built on a simple principle: an agent is not a standalone platform, but one component in a broader system. Every production-grade service—even those powered by AI—relies on databases, logging, authentication, front-ends, and security.

Rather than asking you to migrate your workflow to a new hosted platform, Forma is designed to plug directly into your existing stack.

This philosophy drives several of Forma’s core design choices:

1. **Version Control:** A Forma agent fits naturally within a standard code repository (`git`). Prompts, workflows, and configurations are version-controlled, auditable, and compatible with your existing branching and review workflows.
2. **DevOps-Ready CLI:** The Forma Command-Line Interface (CLI) is the primary interface for working with agents. It runs consistently on your machine and in CI/CD pipelines, enabling seamless automation, testing, and deployment.
3. **Encapsulated Local Development:** During development, dependencies such as databases, front-ends, and monitoring tools are launched as standard Docker containers. This ensures parity between local and production environments and minimizes deployment errors.

In simple terms, Forma does not come

> **Note:** If you’re new to these concepts, don’t worry—we’ll help you get started. But if you’ve worked on any modern cloud-based product, Forma will feel immediately familiar.

## 3. Deploy securely, in your preferred environmnet

We know agents process sensitive data, and we do not want your data! Once you are done defining your agent, we will build a **Docker image** and hand it over to you, so you can deploy it in your own environments, behind whatever security measures you want.

## 4. Test and Evaluate

Our CLI has built-in evaluation support. You can test the agent as a whole, or the [sub components](./building-blocks.md) independently.

## 5. Monitor

The container images we give you have built-in [Opentelemetry](https://opentelemetry.io/) instrumentation, with added [Openinference](https://arize-ai.github.io/openinference) standards so you can analise your traces using [Phoenix Arize](https://phoenix.arize.com). This lets you check integrate Forma agents within your existing observability stack.
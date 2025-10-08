# What is `Archetypes`?

Archetypes is the framework for building production-grade AI agents. We don't build LLMs; we provide the 'system'—the essential guardrails and engineering tools—that lets you harness their full power securely, reliably, and with enterprise-grade explainability.

We operate on simple principles that help you prevent mistakes and maintain the higher standards of security.

## 1. Focus on prompting, not coding

Define and manage complex agent logic using simple, version-controlled `yaml` and `markdown` files. Additionally, our developer tools offer quick hot reloading that let you iterate quickly without getting out of "the zone". These features streamline iteration, minimizes coding errors, and allows your prompt engineers and developers to collaborate seamlessly.

Here is a simple example of an AI Agent.

```yaml
#################################
# Example of a Helpful AI agent.
# Details will be explained later
#################################

id: the-agent # This will show up in observability
start:
nodes:
# Let's talk to Ollama during local development
- llm:
provider: ollama
# This can be put on a separate markdown file, to make it
# more readable and maintainable
system_prompt: 'You are a helpful assistant'
```

## 2. Deploy securely, in your preferred environmnet

We know agents process sensitive data, and we do not want your data! Once you are done defining your agent, we will build a **Docker image** and hand it over to you, so you can deploy it in your own environments, behind whatever security measures you want.

## 3. Test and Evaluate

Our CLI has built-in evaluation support. You can test the agent as a whole, or the [sub components](./building-blocks.md) independently.

## 4. Monitor

The container images we give you have built-in [Opentelemetry](https://opentelemetry.io/) instrumentation, with added [Openinference](https://arize-ai.github.io/openinference) standards so you can analise your traces using [Phoenix Arize](https://phoenix.arize.com). This lets you check integrate Archetypes agents within your existing observability stack.
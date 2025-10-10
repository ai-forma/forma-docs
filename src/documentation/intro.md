# What is `Archetypes`?

> Generative AI really shines at first... but it takes hours of engineering to make it enterprise ready

Archetypes is a framework for building production-grade AI agents. We don't build LLMs; we make them usable in enterprise applications.


<div style="width: fit-content; margin:auto">
    <a style="padding: 0.5em 1em; border-radius:0.5em; background-color:var(--links); color:white;" href="#">Jump to quick start</a>
</div>

Archetypes operates on simple principles that help you avoid mistakes and maintain the higher standards of security.

## 1. Focus on prompting, not coding

Define and manage complex agent logic using simple, version-controlled `yaml` and `markdown` files. Additionally, our developer tools offer quick hot reloading that let you iterate quickly without getting out of "the zone". These features streamline iteration, minimizes coding errors, and allows your prompt engineers and developers to collaborate seamlessly.

Here is a simple example of an AI Agent.

```yaml
id: the-agent # This will show up in observability
start:
nodes:
- llm:
     provider: ollama
   system_prompt: 'You are a helpful assistant'
```

## 2. Deploy securely, in your preferred environmnet

We know agents process sensitive data, and we do not want your data! Once you are done defining your agent, we will build a **Docker image** and hand it over to you, so you can deploy it in your own environments, behind whatever security measures you want.

## 3. Test and Evaluate

Our CLI has built-in evaluation support. You can test the agent as a whole, or the [sub components](./building-blocks.md) independently.

## 4. Monitor

The container images we give you have built-in [Opentelemetry](https://opentelemetry.io/) instrumentation, with added [Openinference](https://arize-ai.github.io/openinference) standards so you can analise your traces using [Phoenix Arize](https://phoenix.arize.com). This lets you check integrate Archetypes agents within your existing observability stack.
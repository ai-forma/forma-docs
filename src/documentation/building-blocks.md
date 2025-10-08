# Core Concepts

Archetypes is built around a small set of concepts. By understanding these, you can read, write, and reason about any agent you define. Having a small set of concepts also helps understand traces and debug information better.

## 1. LLMs

The lowest level of an Archetype agent is the Large Language Model (LLM) client, which we just call 'LLM'. This is a small machine that sends a set of messages to an LLM provider (e.g., Claude, Gemini, OpenAI or Ollama) in order to produce a response.

Different providers (OpenAI, Anthropic, Ollama, etc.) can be swapped in and configured without changing your agent’s logic.

## 2. Nodes

A **Node** is the basic building block of a workflow. Each node always follows the same steps:

1. **Triage** – an LLM takes the context decides what to do next, based on the full conversation context. It might choose to respond right away, or call tools.
2. **Tools (optional)** – If the LLM decided that one of its available tools would be useful to comply with the client's request, the node will call them.
3. **Summarisation** – If tools were invoked, the node will call an LLM again, in order to respond to the client appropriately, with the new information provided by the tools. (**Note**: This can be skipped if only a single tool is called, and such tool is marked as `not-summarize`. This is useful in many situations, as will be explained in the [Tools](tools.md) section)

Key points to remember:

- Nodes _always_ triage.
- Tools may or may not be executed. Specifically, there is no guarantee that a specific tool will be ran and thus it is important that its output is not required downstream.
- Summarisation will not run if no tools were called of it the tools called are marked as `not-summarize`.
- Both the Triage and Summarise have access to the **entire context** (conversation history, prior tool outputs, etc.).

## 3. Workflows

**Workflows** are a mechanism to break down large tasks into smaller—more focused—tasks. This is beneficial because complicated tasks—which require very large system prompts—and thus the AI Models will struggle to follow those instructions faithfully. By breaking down a big task into smaller bits, you can provide more precise, prevent contadictions in your prompts. Like people, LLMs perform better with clear and focused instructions.

A **Workflow** is a set of nodes that depend on each other (for the Geeks, it is a Directed Acyclic Graph of nodes). 

> **Example**
> 
> We can break down this: 
> 
> ```
> Take this academic article and produce a blog post for 5th-graders, 
> in Spanish. 
>
> The content of the blog post should include a brief 
> introduction/motivation, a brief explanation of the methodology,
> and an emphasis in the results and implications.
>  
> Your target audience is 5th graders, so do not use acronyms or jargon.
> Use examples to make it more relatable.
> ```
> 
> Into these more focused steps
> 
> 1. `Create a list containing the (1) motivation; (2) methodology; (3) results and implications from the following paper` 
> 2. `Write a blog post for 5th graders based on the following summary points. Explain the motivation, outline the methodology and emphasise the results and implications. Use examples to make it more relatable.` 
> 3. `Translate this blog post into Spanish. Keep the tone and length of the post.`


An interesting feature is that a workflow can itself be exposed as a **tool**. This means that a node can decide to call a completely different worflow and then use its output to answer a question. For instance, the example above—the workflow that writes blog posts based on academic papers—could be a tool within a larger AI Agent that cannot only do that, but also other tasks (e.g., write abstracts or format references). This makes workflows both composable and reusable, and let Archetype agents implement complex logic at scale.

> **Note**: When a workflow is used as a tool, it does not receive the whole conversation with the client..


## 4. Agents

An agent is a wrapper of a root Workflow and a set of configuration parameters.


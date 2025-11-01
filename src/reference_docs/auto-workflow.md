# Workflow

Workflows are a mechanism to break down large tasks into smaller—more focused—tasks. This is beneficial because complicated tasks—which require very large system prompts—and thus the AI Models will struggle to follow those instructions faithfully. By breaking down a big task into smaller bits, you can provide more precise, prevent contadictions in your prompts. Like people, LLMs perform better with clear and focused instructions.

A Workflow is a set of nodes that depend on each other (for the Geeks, it is a Directed Acyclic Graph of nodes).

After its execution, a Workflow returns an object with the results of
its output nodes.


## Full Specification

```yaml
id: string
nodes: 
	- Node
	- ...
output: WorkflowOutput # optional
evals: 
	- Eval
	- ...
```

#### `id`

The ID. If absent, one will be provided.

#### `nodes`

The nodes within the Workflow. All nodes
needed to generate the outputs are guaranteed
to run.

#### `output` (*optional*)

The IDs of the nodes that will end up in the output
provided by this workflow.

#### `evals`

The names of the evaluations to be ran for this workflow



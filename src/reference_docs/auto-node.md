# Node

A Node is the key of Forma Agents\' execution. They are the
ones that call LLMs, process their response, and decide whether
tools should be called. It always does the same thing:

1. **Triage** – an LLM takes the context decides what to do next, based on the full conversation context. It might choose to respond right away, or call tools.
2. **Tools (optional)** – If the LLM decided that one of its available tools would be useful to comply with the client\'s request, the node will call them.
3. **Summarisation** – If tools were invoked, the node will call an LLM again, in order to respond to the client appropriately, with the new information provided by the tools. (**Note**: This can be skipped if only a single tool is called, and such tool is marked as `not-summarize`. This is useful in many situations, as will be explained in the [Tools](tools.md) section)


## Full Specification

```yaml
id: string
llm: GenaiClient
system_prompt: string
summarization_llm: GenaiClient # optional
summarization_prompt: string # optional
tools: 
	- TemplateField
	- ...
evals: 
	- Eval
	- ...
triage_evals: 
	- Eval
	- ...
summarize_evals: 
	- Eval
	- ...
```

#### `id`

The ID of the node. If absent, one will be provided.
The value given here is used to identify the output
of this node in subsequent nodes within a workflow,
allowing for template interpolation

#### `llm`

The main LLM and settings to use for triage and

#### `system_prompt`

The main instruction given to the LLM.

#### `summarization_llm` (*optional*)

An optional LLM for summarisation. If this is not there,
summarisation will be done using the main llm.

#### `summarization_prompt` (*optional*)

An optional instruction for summarization. If absent,
the `system_prompt` will be used

#### `tools`

The tools that the LLM can decide to call.

#### `evals`

The evaluations used to test this specific node as a
whole (different from Triage- and Summarize-specific evals)

#### `triage_evals`

The evaluations used to test the triage LLM specifically

#### `summarize_evals`

The evaluations used to test the summarize LLM specifically



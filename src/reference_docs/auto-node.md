# Node



## Full Specification

```yaml
id: string
llm: GenaiClient
system_prompt: string
summarisation_llm: GenaiClient # optional
summarisation_prompt: string # optional
tools: 
	- TemplateField
	- ...
evals: 
	- Eval
	- ...
```

#### `id`


#### `llm`

The main LLM and settings to use for triage and

#### `system_prompt`


#### `summarisation_llm` (*optional*)

An optional LLM for summarisation. If this is not there,
summarisation will be done using the main llm.

#### `summarisation_prompt` (*optional*)


#### `tools`


#### `evals`

The evaluations to run



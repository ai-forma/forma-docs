# ToolWorkflow



## Full Specification

```yaml
id: string
nodes: 
	- Node
	- ...
output: WorkflowOutput # optional
input_prompt: string
evals: 
	- Eval
	- ...
```

#### `id`


#### `nodes`


#### `output` (*optional*)


#### `input_prompt`

determines the schema and the messsate that will be used
to trigger this workflow execution as a tool

#### `evals`

The names of the datasets containing evaluation data



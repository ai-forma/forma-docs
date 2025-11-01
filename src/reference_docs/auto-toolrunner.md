# ToolRunner

A tool runner lets you select one of the several tools
that are built into Forma. They will handle the communication
with the LLM (in terms of inputs and outputs)


## Supported Variants

> 🎯 Variants are identified by using the `type` field. For instance 
>
> ```yaml
> type: name-of-variant
> ```

### [`template`](./auto-templatetool.md)
Takes a template, asks the LLM to generate
its fields, and returns a String with the rendered
template
### [`workflow`](./auto-workflowtool.md)
Runs a workflow as if it was a tool, using a fresh
state (i.e., does not receive the whole conversation)

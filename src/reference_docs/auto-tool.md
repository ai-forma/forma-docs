# Tool

Tools are instruments that allow AI Agents do things.
They way they operate is that we send an LLM a request,
and in that request we include the possible actions we
have available for taking. The LLM will *not* execute any
action (Forma does it afterwards) but it can decide *which*
tool and its arguments.

The purpose of this Tool object is to describe the possible
actions to the LLM, so it can decide.


## Full Specification

```yaml
name: string
description: string # optional
tool: ToolRunner
```

#### `name`

The name of the tool. Should be descriptive to the LLM
so it can discriminate between tools.

(Misleading names just cause confusion)

#### `description` (*optional*)

A more detailed description of the tool, for the LLM to
discriminate between options.

#### `tool`

The Tool that will be executed if the this tool
is selected.



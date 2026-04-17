# TemplateTool

This tool asks an LLM to fill the missing fields on a template.

This tool receives one or more templates, all of which share the same
field specifications (e.g., they all have the same fields with the same
types and descriptions). At runtime, it randomly selects one of the
templates and asks the LLM to populate it.

This tool is useful for defining pre-defined responses that should
not feel too robotic (e.g., \"The current time is {{time: string}}\" and \"It is
{{time: string}}\") and for mocking up responses (e.g., \"I checked your
email, there are no new messages from {{address}}\" vs \"You do not have
any new messages from {{address}}\")


## Full Specification

```yaml
templates: 
	- string
	- ...
```

#### `templates`

The templates to choose from. For instance,

> hello {{name: string \"the name of the user\" }}, nice to meet you! The current time is {{time: string \"the current time\"}}



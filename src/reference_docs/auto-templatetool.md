# TemplateTool

This tool asks an LLM to fill the missing fields on a template.

It will take a template with certain field specifications,
and will ask the LLM to populate it.


## Full Specification

```yaml
template: string
```

#### `template`

The template to fill. For instance,

> \"hello {{name: string \"the name of the user\" }}, nice to meet you! The time is {{time: string \"the current time\"}}\"



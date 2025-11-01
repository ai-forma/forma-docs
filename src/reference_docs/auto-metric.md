# Metric

A metric utilized to judge the response given by an AI
Agent.

To scale it properly, the Judge will be an LLM itself


## Full Specification

```yaml
judge: GenaiClient
template: string
```

#### `judge`

The `GenaiClient` that will judge the response according
to the template above.

#### `template`

Metric templates can contain three fields:

1. `actual_output` - Which will be replaced with the answer of the agent, node or other.
2. `input` - Which will be replaced by the input, extracted from the dataset.
3. `expected_output` - An optional value, that would also be extracted from the example.

They will produce the following outputs:

1. `label` - A single-word verbal equivalent of the score (e.g., \'Good\', \'Bad\', \'Hallucination\'). Base this value on the instructions provided
2. `score` - The numerical value reflecting the quality of the evaluation, assigned as per the instructions
3. `explanation` - A verbal explanation for the score and labels given

For example:    

> Your job is to judge whether this sentence:
>
> {{actual_output}}
>
> (1) a good answer th the following question:
>
> {{input}}
>
> and (2), whether contradicts this reference answer:
>
> {{expected_output}}
>  
> Give it a score between 0 and 2 (one point for each
> criteria), explain your reasoning behind the score,
> and indicate whether it is Horrible (0 points), Bad (1 point)
> or Good (2 points)



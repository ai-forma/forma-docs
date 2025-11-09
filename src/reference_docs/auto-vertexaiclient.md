# VertexAIClient

A client for calling Google Cloud\'s Vertex AI models.

> 🔑 **Authentication**: Work in progress... we aim to use the GCloud Credentials
> as stored in the machine

> Note: the documentation below has been copied nearly verbatim
> from Google Cloud\'s documentation.


## Full Specification

```yaml
model: string
location: string
cached_content: string # optional
tools: 
	- Tool
	- ...
tool_choice: Mode # optional
temperature: number # optional
top_p: number # optional
top_k: number # optional
candidate_count: i32 # optional
max_output_tokens: i32 # optional
stop_sequences: 
	- string
	- ...
response_logprobs: boolean # optional
logprobs: i32 # optional
presence_penalty: number # optional
frequency_penalty: number # optional
seed: i32 # optional
response_mime_type: string
response_format: JsonSchema # optional
include_thoughts: boolean # optional
thinking_budget: i32 # optional
image_aspect_ratio: string # optional
```

#### `model`

The model to use. Check Google Cloud\'s availability
of models in different regions

#### `location`

The location of the endpoint to use (e.g., \'global\', \'us-central1\')

#### `cached_content` (*optional*)

The name of the cached content used as context to serve the
prediction. Note: only used in explicit caching, where users can have
control over caching (e.g. what content to cache) and enjoy guaranteed cost
savings.

It is assume to be cached in the same project and location as the Vertex
AI client

#### `tools`

A `Tool` is a piece of code that enables the system to interact with
external systems to perform an action, or set of actions, outside of
knowledge and scope of the model.

#### `tool_choice` (*optional*)

Which tools to call, if any. Options are:
- `auto`: Default model behavior, model decides to predict either function calls or natural language response.
- `any`: Model is constrained to always predicting function calls only. If \"allowed_function_names\" are set, the predicted function calls will be limited to any one of \"allowed_function_names\", else the predicted function calls will be any one of the provided \"function_declarations\".
- `none`: Model will not predict any function calls. Model behavior is same as when not passing any function declarations.

#### `temperature` (*optional*)

Controls the randomness of predictions.

#### `top_p` (*optional*)

If specified, nucleus sampling will be used.

#### `top_k` (*optional*)

If specified, top-k sampling will be used.

#### `candidate_count` (*optional*)

Number of candidates to generate.

#### `max_output_tokens` (*optional*)

The maximum number of output tokens to generate per message.

#### `stop_sequences`

Stop sequences.

#### `response_logprobs` (*optional*)

If true, export the logprobs results in response.

#### `logprobs` (*optional*)

Logit probabilities.

#### `presence_penalty` (*optional*)

Positive penalties.

#### `frequency_penalty` (*optional*)

Frequency penalties.

#### `seed` (*optional*)

Seed.

#### `response_mime_type`

Output response mimetype of the generated candidate text.
Supported mimetype:

- `text/plain`: (default) Text output.
- `application/json`: JSON response in the candidates.
  The model needs to be prompted to output the appropriate response type,
  otherwise the behavior is undefined.
  This is a preview feature.

#### `response_format` (*optional*)

The `Schema` object allows the definition of input and output
data types. These types can be objects, but also primitives and arrays.
Represents a select subset of an [OpenAPI 3.0 schema
object](https://spec.openapis.org/oas/v3.0.3#schema).
If set, a compatible response_mime_type must also be set.
Compatible mimetypes:
`application/json`: Schema for JSON response.

#### `include_thoughts` (*optional*)

Optional. Config for thinking features.
An error will be returned if this field is set for models that don\'t
support thinking.
Indicates whether to include thoughts in the response.
If true, thoughts are returned only when available.

#### `thinking_budget` (*optional*)

Optional. Indicates the thinking budget in tokens.
This is only applied when enable_thinking is true.

#### `image_aspect_ratio` (*optional*)

 The desired aspect ratio for the generated images. The following
aspect ratios are supported:

\"1:1\"
\"2:3\", \"3:2\"
\"3:4\", \"4:3\"
\"4:5\", \"5:4\"
\"9:16\", \"16:9\"
\"21:9\"



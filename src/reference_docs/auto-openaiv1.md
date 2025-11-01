# OpenaiV1

A client for OpenAI\'s v1 api

It attempts to adhere as strictly as possible (even if
some features are not supported by Forma).

> 🔑 **Authentication**: uses the `OPENAI_API_KEY` API Key

> Note: the documentation below has been copied nearly verbatim
> from OpenAI\'s one, as reference


## Full Specification

```yaml
endpoint: string
model: string
audio: OpenAIAudioSettings # optional
frequency_penalty: number # optional
logprobs: boolean # optional
max_completion_tokens: int # optional
metadata: serde_json # optional
modalities: 
	- OpenAIModality
	- ... # optional
n: int # optional
parallel_tool_calls: boolean # optional
presence_penalty: number # optional
prompt_cache_key: string # optional
reasoning_effort: OpenAIReasoningEffort # optional
response_format: OpenAIResponseFormat # optional
safety_identifier: string # optional
service_tier: OpenAIServiceTier # optional
store: boolean # optional
stream: boolean # optional
stream_options: OpenAIStreamOption # optional
temperature: number # optional
text: OpenAITextField # optional
tool_choice: OpenAIToolChoiceMode # optional
tools: 
	- OpenAITool
	- ... # optional
top_logprobs: int # optional
top_p: number # optional
```

#### `endpoint`

The endpoint to reach for the API. Defaults to `https://api.openai.com`

#### `model`

The model to use. Defaults to `gpt-3.5-turbo`

#### `audio` (*optional*)

Required when audio output is
requested with `modalities: [\"audio\"]`.

#### `frequency_penalty` (*optional*)

Number between -2.0 and 2.0. Positive values penalize new tokens
based on their existing frequency in the text so far, decreasing
the model\'s likelihood to repeat the same line verbatim.

#### `logprobs` (*optional*)

Whether to return log probabilities of the output tokens or not.
If true, returns the log probabilities of each output token
returned in the content of message.

#### `max_completion_tokens` (*optional*)

An upper bound for the number of tokens that can be generated for a
completion, including visible output tokens and reasoning tokens.

#### `metadata` (*optional*)

Set of 16 key-value pairs that can be attached to an object. This can
be useful for storing additional information about the object in a
structured format, and querying for objects via API or the dashboard.

Keys are strings with a maximum length of 64 characters. Values are
strings with a maximum length of 512 characters.

#### `modalities` (*optional*)

Output types that you would like the model to generate. Most models are
capable of generating text, which is the default

#### `n` (*optional*)

How many chat completion choices to generate for each input message.
Note that you will be charged based on the number of generated tokens
across all of the choices. Keep `n` as `1` to minimize costs.

#### `parallel_tool_calls` (*optional*)

Whether to enable [parallel function calling](https://platform.openai.com/docs/guides/function-calling#configuring-parallel-function-calling)
during tool use

#### `presence_penalty` (*optional*)

Number between -2.0 and 2.0. Positive values penalize new tokens
based on whether they appear in the text so far, increasing the
model\'s likelihood to talk about new topics.

#### `prompt_cache_key` (*optional*)

Used by OpenAI to cache responses for similar requests to optimize
your cache hit rates. Replaces the user field. [Learn more](https://platform.openai.com/docs/guides/prompt-caching).

#### `reasoning_effort` (*optional*)

Constrains effort on reasoning for reasoning models. Currently supported
values are minimal, low, medium, and high. Reducing reasoning effort
can result in faster responses and fewer tokens used on reasoning in a response.

#### `response_format` (*optional*)

An object specifying the format that the model must output.

Setting to `{ \"type\": \"json_schema\", \"json_schema\": {...} }`
enables Structured Outputs which ensures the model will match your
supplied JSON schema.

Setting to `{ \"type\": \"json_object\" }` enables the older JSON mode,
which ensures the message the model generates is valid JSON.

Using `json_schema` is preferred for models that support it.

#### `safety_identifier` (*optional*)

A stable identifier used to help detect users of your application
that may be violating OpenAI\'s usage policies. The IDs should be a
string that uniquely identifies each user. We recommend hashing their
username or email address, in order to avoid sending us any identifying
information.

#### `service_tier` (*optional*)

When the `service_tier` parameter is set, the response body will
include the `service_tier` value based on the processing mode actually
used to serve the request. This response value may be different from
the value set in the parameter.

#### `store` (*optional*)

Whether or not to store the output of this chat completion request
for use in our model distillation or evals products.

Supports text and image inputs.
**Note**: image inputs over 10MB will be dropped.

#### `stream` (*optional*)

If set to true, the model response data will be streamed
to the client as it is generated using server-sent events.
See the Streaming section below for more information,
along with the streaming responses guide for more information
on how to handle the streaming events.

#### `stream_options` (*optional*)


#### `temperature` (*optional*)

What sampling temperature to use, between 0 and 2. Higher values like 0.8 will make
the output more random, while lower values like 0.2 will make it more focused
and deterministic. We generally recommend altering this or top_p but not both.

#### `text` (*optional*)

Constrains the verbosity of the model\'s response. Lower values
will result in more concise responses, while higher values will
result in more verbose responses. Currently supported values are
`low`, `medium`, and `high`.

#### `tool_choice` (*optional*)

Controls which (if any) tool is called by the model. `none` means
the model will not call any tool and instead generates a message.
`auto` means the model can pick between generating a message or calling
one or more tools. `required` means the model must call one or more tools.

#### `tools` (*optional*)

A list of tools the model may call.

#### `top_logprobs` (*optional*)

An integer between 0 and 20 specifying the number of most
likely tokens to return at each token position, each with an
associated log probability. logprobs must be set to true if
this parameter is used.

#### `top_p` (*optional*)

An alternative to sampling with temperature, called nucleus sampling,
where the model considers the results of the tokens with top_p probability
mass. So 0.1 means only the tokens comprising the top 10% probability
mass are considered.

We generally recommend altering this or temperature but not both.


